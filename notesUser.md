## Notes for Users
If you are an experienced user and want to change the ontology/questions, etc. read this document.

### Ontology
Ontology describes the types of document you want to store (called docTypes) and their properties. A docType of "sample" might have a property "name". The ontology is designed to be completely flexible with only rules on naming. Read the default doctypes and their properties to get a picture.

#### Rules for document types
- docType is the "sample", "instrument", ... Doctypes are lowercase; cannot start with 'x','_', numbers, no spaces.
- different properties of a doctype can be separated with a heading to add structure.
  - Example of doctype: Sample
    - Heading "Geometry" with properties height, width, length
    - Heading "Identifiers" with properties name, qr-code

###### Special document types
- "x0", "x1", "x2", ... is the names of the folder/directorys on the hard-disk. Every other doctype should belong to (at least) one project=x0.
- "measurement" corresponds to a file on the disk. When scanning for new files, "measurement" is the default doctype. Other docTypes can have also connected files.

##### Other doctypes
- "sample" and "procedure" are ordinary doctypes. The doctypes "sample" and "procedure" correspond to the information found in the methods section of a publication. **The minimalist statement of research: A "sample" was studied by the "procedure" to obtain the "measurement".**
  - procedure
    - standard recipes with instrument information, e.g. Bake the cake at 200-210C
    - the revision number can be added as field
  - measurements
    - precise configuration of the measurement and any deviations from the procedures, aka used "200C" as temperature.
    - have hierarchical types: e.g. length measurements, meter measurements, ...
    - link to calibration measurements possible
  - sample
    - link to other/previous samples is possible


#### Rules for properties
1. name: alpha-numeric, no spaces
  - forbidden names: branch, type, user, client
2. query: long description including spaces
  - if omitted: user is not asked about this property (those that are filled automatically)
3. list: list of options
  - Important: a list is always better than no list. It gives user specific choices and prevents typos.
  - list of options in text form ['hammer','saw','screwdriver']
  - list of other doctypes, e.g. list of samples, to link to those
4. required: if this property is required
   if omitted: required=false is assumed
5. unit: a unit of property, e.g. 'm^2'
   - if present: entered value is a number (not enforced yet)
   - if omitted: entered value is a text

##### Special properties
- Don't add 'project' etc. as property as it is added automatically (during the creation of the forms and then processed into branch.)
- "comment" is a remark which has additional functions. If you enter "#tag" in it or ":length:2:", these are
  automatically processed. If not present, a comment will be added to all doctypes.
- "content" is displayed in a pretty fashion and it is a markdown formatted text. This is a very optional property.
- "tags" is added automatically if those tags are found in comments
- "curated" is added automatically if the document was edited
- "image" is optional but should be base64 encoded string
- "name" is optional but generally helpful. Alternative meanings of name: specimen-id.


