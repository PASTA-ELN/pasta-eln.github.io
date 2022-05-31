# The layout of PASTA database
## Data storage
- The filesystem is the general storage of data.
- DataLad allows the revision and inclusion of large external data. This is efficient and does not change the filesystem as general storage.
- A DataLad dataset can be projects, steps, task
- Data are measurements, Standard-Operating-Procedures, Sample-Figures, ...
- Project management (Projects, Steps, Tasks) form a hierarchical folder structure.
- Local filesystem
  - gives user incentive to use structure
  - to allow the user to drop in files
  - raw data can be stored here (.tif, .mss)
- Completely external data is possible as link and authorization is stored
## Metadata storage
- Stored as CouchDB as most flexible as metadata for different experiments necessarily differs
- Project management (Project, Steps, Task) is included in metadata storage
- The result of curation "Low-quality image" is stored
## Bracket across data and metadata storage
- Python backend that allows extractors (default and custom) for metadata from measurement files
- Python-Command-Line-Program interacts between user and backend
- React-Electron programs (GUI) interact in between user and backend
- All these form superlayer ontop of Metadata and Data storage
## Access Control and Authorship
- Layout depends on the filesystem, DataLad/Git and CouchDB; each has Access Control (read,write access)
- Software only has to interact with these (existing) access-control concepts
- Authorship is saved in data and meta-data automatically for data and semi-automatically for meta-data
- The authorship can be stolen in any case: "If I can read a file, I can copy/screenshot it and claim it is mine". The only weapon against authorship thieves is publishing to _trusted_ 3rd parties (journals, DataLad/Git repositories).
- Only one author/user PID has to be stored, e.g. ORCID-ID
## Revision control is included
- in data and metadata storage
