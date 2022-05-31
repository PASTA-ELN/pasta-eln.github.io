## CouchDB information
Here we discuss design concepts of the chosen database and why we choose the CouchDB implementation


### FAQs
#### Why choose a NoSQL database and not a SQL database
- NoSQL databases (CouchDB, MongoDB)
  + are good for unstructured data. As such any document/information can be added. This is very beneficial in scientific environments and ELNs in particular since the structure is not fixed.
  + are a little slower when creating tables. This drawback is not so relevant for ELNs. However, if you are a bank with millions of customers, you want to scan that database fast.
- SQL databases (Oracle, MySQL, ...)
  + are good for structured data and metadata. Bank customers all have a name, address, portfolio value, ...
  + Could be appropriate for a lab-assistant structure in which 10 technicians create data according to fixed protocols and a single person digests it.

#### Why did we choose CouchDB and not MongoDB?
- The REST-API for CouchDB exists and that feature allows fast development of HTML pages, mobile access....
- The REST-API for MongoDB has to be written using a nodeJS server and should follow the same protocol as the REST-API for CouchDB.
Once the version of CouchDB is operational, the MongoDB API can be written and one could switch to MongoDB, which might have advantages in the future.

#### How is hierarchical information stored
One part of PASTA is the hierarchical information: a project is the "parent" of everything, task is a "child", a subtask is a "grandchild" in computer language. There are two possibilities to create this structure in a flat database:
##### Case 1 - upward linking: "I am the child of ..."
  - The difficulty in this setup is that one needs to account for the order of child.
  - Hence two fields are required: ancestors tree (or only parent) and child-number ["I am the 3rd child"]
  - This approach is used in PASTA: "stack" has the id-numbers of the ancestors and childNum is count
##### Case 2 - downward linking: "I have these children [list of children]"
  - Advantage: only order of children required and these are only stored once.
  - Disadvantage: adding one child requires that the parent is changed: it has a new child
  - Disadvantage: for fast indexing and table building, each person should know the project ID. This is not stored in this approach and hence an additional field would be required.
  - This approach was used in very early versions of PASTA until the 2nd disadvantage was identified.
##### Implementation details
- "path", "child-number" and "stack of id-numbers" (parental hierarchy) form a branch
- a measurement, sample, procedure can have multiple branches
  as the scientist can use a measurement in different projects.
- Projects/tasks/subtasks only have one branch as they are only existant in a project.

#### What data is stored:
Different types of data (different document types) are stored in the database:
- text items: projects, tasks, subtasks
- data: samples, procedures
- automatically added: measurements

Other things don't need to be stored:
- own papers (is an automatic result of projects)
- presentations (is an automatic result of projects)
- literature database: belong to project, can be searched anyhow




### Database design technical details:
All documents have the following properties
- type is a list of hierarchical types:
  - examples for most data: ["measurement", "Zeiss tif image"], ["measurement", "Indentation", "Pop-in study"]
  - text items (projects, tasks) are ["x0"], ["x1"], ... as the types are non hierarchical in the class view (IT-term). A task is not a special class of the project class. Moreover, the hierarchical level is engrained in the type
- Tags #tag, #1 (no spaces in the string). #1 implies one-star, #2 implies two-stars. Tags are stored as list of stings.
- other fields can be easily added in the comment field of the form and are thereafter separated. Examples for other fields:  :BakingTime:2h: :quality:3:  (':' is a marker here)
- Comments
  - If the user enters a comment in the comment field: tags and fields are substracted and everything that remains is the comment
  - Comments should be in the Markdown format (Pandoc flavor)
- List of branches: each branch has a path (link to the file on disk, remote url), its hierarchy-stack and the number of this child
- all data should be saved in SI units or specified

#### Examples
Essential items have a preceding '-'
Samples:
- {-type:["sample"], -name: "sample1", chemistry: "Cu50Co50", origin: "deposition in oven", size: "3 x 3 mm"}

Procedures:
- {-type:["procedure", "EM"], -name: "How to do TEM", content: "Arbitrary text in md-format including \n", tags: ["#TEM"]}


Text/Hierarchical entries: Project, Tasks
- {-type:["x0"], -name: "Identify phase", objective: "Identify phase at boundary", status: "active", tags: ["TEM","experiments"]}
- {-type:["x1"], -name: "Inspect in TEM", comment: "Text in md-format including \n", tags: ["TEM"]}
- {-type:["x2"], -name: "Inspect in TEM on Monday", text: "Text in md-format including \n", tags: ["TEM"], procedure:link to #id}

Measurements
- {-type: ["measurement", "Zeiss"], -branch:{path:<link>}, producer: Zeiss, SHASUM: "43aa", comment:"Ugly picture"}
- {-type: ["measurement", "Zwick"], -branch:{path:<link>}, producer: Zwick, SHASUM: "43aa", comment:"Slip in grips"}
- {-type: ["measurement"], Youngsmodulus: "300GPa", Hardness "10GPa"}
- All measurements have an SHASUM of their original state (Git-shasum see [dataLad](dataLad.md)) to ensure that the data is not changed from its original state. DataLad has an additional mechanism to ensure data integrity.

#### Views
Views are tables that are created automatically and are rather fast. The following items should be in each table/view.
- ProjectID should be the key in each view to allow for easy filtering
- all project headers form a view for the project overview
- a hierarchical tree of a given project
- all procedures,... are assembled in a view
- all tags are assembled in a view and can be used in future to find items fast
