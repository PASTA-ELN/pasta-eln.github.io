# Introduction
This is detailed information for developers.

## Software design and unit tests
The different parts of the PASTA database framework are shown in the [scheme](pastaScheme.png). The user interacts with the blue parts; the purple dashed-arrow shows how metadata is generated.

The dots mark which parts are tested automatically by end-to-end user tests.
- React-DOM and React-Electron have most things in common; therefore not all items have to be tested in React-Electron
- React-DOM test all clicks/events using the cypress framework (test script is not in Git-repository since it includes passwords)
- React-Electron has no easy testing (to my knowledge). General program automation using python could be used, but require that the window is at the same spot.
- Python (pastaDB.py) is extensively tested.
- There is a global script, that executes all other scripts. That global script is not part of the Git-repository.

## Ontology and design
All metadata for the different documents is defined only by JSON strings in the data-dictionary/scheme. The data-dictionary is stored in the database and can be adopted  *manually/automatically* over time. Documents have different types (e.g. measurement), which can have subtypes (e.g. electron microscopy image).

There are reserved names that the user should not use, e.g. branch, image, ...

## Common code-parts (commonTools.js) should be common
### written in js and automatically translated to python
+ filling/verification of fields in commonTools.js
+ imported everywhere
+ JSON objects move information between parts
+ commonTools.js is automatically translated to python and can be used there.
+ Same code, same function [no update delays]
  - all UUIDs include the document type: change UUID to m-UUID
    not sure if required but does not hurt and allows verification
### variables outside of the commonTools
- Dictionary: Database information: URL, password, user-name
- Dictionary: documentype,documentlabel
- List: Hierarchy
- Questions for this datatype:
- current document: self.doc
- current view: viewTable
### Individual code has to be individual
+ Storage: use same names
  - python: backend.class
  - reactDOM: flux-storage
  - reactNative: async-storage

* * *

## Python
### Data stored
- python: questionary CLI
- Directories: self.softwareDirectory; self.cwd; self.baseDirectory
- Editor arguments: self.eargs   = configuration["eargs"]
- Next choices in sequential questions: self.nextChoicesID, self.nextChoices
- List: Hierarchy stack: self.hierStack
- Leave top-level-questions-variable in CLI
  since online versions never need all questions.

### Unit-test in python
- Command "python3 -m unittest discover -s Tests"
  - verifies that output checkDB has no errors
  - verifies that log-file has no errors or warnings
- during database verification
  - sha-sum of measurement not changed, i.e. file not altered
  - the revision-history of the metadata is recorded

#### Install dependencies for some of the tested data
use Git to install in some location
```bash
git clone https://jugit.fz-juelich.de/s.brinckmann/experimetal-micromechanics
```

#### Ensure that the path to experimental-micromechanics is in your python path
open python
```python
from Tif import Tif
from nanoIndent import Indentation
```

#### Run unit test in PASTA's python folder
- run unit-test in main python folder to test installation
```bash
python3 -m unittest discover -s Tests
```

### Python: how to debug in Linux
```bash
pudb3 ./pastaCLI.py
pudb3 Tests/testBasic.py
```
scrolling and up/down keys allow to move ahead and set a breakpoint
? help; n next line; s step into; c continue
q quit
o showOutput;
left/right keys move to variables
Ctrl-X: command-line: full interaction with variables
### Python: how to debug in Windows
```python
import traceback
...
### FOR DEBUGGING WINDOWS
print('\nStack:\n  '+'\n  '.join([item.split('\n')[0].strip() for item in traceback.format_stack()[11:]]))
print('More comments')
os.system("pause")
```

Windows file permissions...
```python
print(win32api.GetFileAttributes(self.basePath+path+os.sep+'.id_pasta.json'))   #tells windows permission, if hidden (32), cannot write
print(os.access(self.basePath+path+os.sep+'.id_pasta.json', os.R_OK))         #does not help, inform
```
* * *

## JavaScript and React
### Design color choices
  colorLight: #f8f5f0
  colorDark: #8e8c84
  black: #3E3F3A;
### Data stored
- reactDOM: html, css, flux-action-dispatcher
- reactNative: its elements/screens and react-navigation
### Notes React-DOM
- allows to develop with react-bootstrap and fast reload
- debugging with Developer tools (Debug->Webpack->src)
  - double click to set break points
  - not very convenient but does the trick
  - if it leaves the track during stepping, error has occurred
- constructor has only default values; componentDidMount has all the initial work functions (fill with data from other sources)
### Notes React-Electron
- allows to develop with react-bootstrap and fast reload
  - sometimes hot-reload breaks: restart with 'npm start'
- debugging with Developer tools (Debug->Webpack->src)
  - double click to set break points
  - not very convenient but does the trick
  - if it leaves the track during stepping, error has occurred
- constructor has only default values; componentDidMount has all the initial work functions (fill with data from other sources)
- Suggestion: create symbolic links to corresponding files in the ReactDOM version. This action results in "git status" will show "typechange". But one can easily ignore them. Benefit: one only has to change one version.

* * *

## Misc notes on design choices
### Automatic unit testing with GitLab CI is difficult
  - see GitLab-ci.yml
  - existing CouchDB instance has to run (one can use an external one, e.g. ibm)
  - fileSystem operations have to be moved away from home to based on TestDirectory
  - credentials of autotest have to be established

### x-UUID is required
  - allows easy debugging, searching in a database
  - types and subtypes: how structured or unordered with just m-; s-; p-;

### Images/Thumbnails as an attachment
If they become an attachment, then images are not automatically included in get-document

### Perhaps change to the front system for the backend
  - makes choice tree longer: output and edit both benefit from chosen project
  - simplifies edit and setEditString

### Datalabels and types: no spaces inside them

### commontools.js bug/feature
  - Tags: #3 #d
  - Some tags disappear: "#d" should not be used, since I do not see the point in short tags

### Additional fields are not shown in project head.
  - would requried additional code, not sure how important this case is

### Notes
update conflict means I cannot update document since you did not specify _rev


* * *

## How to setup a remote couchDB server
### Simplify curl commands
```bash
export db=http://134.94.32.112:5984
cat > ~/.curlrc
-s
-H Accept:application/json
-H Content-Type:application/json
```

### User
#### New users
Create users: name and _id must correspond. You can also do it via CouchDB GUI
```bash
curl -u **ADMINISTRATOR**:**PASSWORD** -X POST $db/_users/_bulk_docs -d @- << EOF
{"docs": [
    {"_id": "org.couchdb.user:s.brinckmann", "name": "s.brinckmann", "password": "test1234", "roles": ["pasta_tutorial-W"], "type": "user", "orcid": "**ORCID**"},
    {"_id": "org.couchdb.user:testReader", "name": "testReader", "password": "test1234", "roles": ["pasta_tutorial-R"], "type": "user", "orcid":""}
]}
EOF
```
#### Users: add roles /small changes
make those in CouchDB GUI

### Database
(Note: could be scripted as only admin,password and database are required)
1. create database by GUI or manually
```bash
curl -u **ADMINISTRATOR**:**PASSWORD** -X PUT $db/**NAME**
```

2. create *_security* in database
```bash
curl -u **ADMINISTRATOR**:**PASSWORD** -X PUT $db/**NAME**/_security -d @- << EOF
{
    "admins": {
        "names": [],
        "roles": ["**NAME**-W"]
    },
    "members": {
        "names": [],
        "roles": ["**NAME**-R"]
    }
}
EOF
```

3. create *_design/authentication* in database
```bash
curl -u **ADMINISTRATOR**:**PASSWORD** -X PUT $db/**NAME**/_design/authentication -d @- << EOF
{
   "validate_doc_update": "function(newDoc, oldDoc, userCtx) { if (userCtx.roles.indexOf('**NAME**-W') !== -1) { return; } else { throw ({ unauthorized: 'Only Writers (W) may edit the database' }); } }"
}
EOF
```

### Other information on curl commands
Configuration has all information one needs in one json-string
"remote_pasta_tutorial": {
    "user": "",
    "password": "",
    "url": "http://134.94.254.66:5984",
    "database": ""
  },

Anybody write
```bash
curl -X PUT $db/pasta_tutorial/testDocument
```
Output: {"error":"unauthorized","reason":"You are not authorized to access this db."}

Reader write
```bash
curl -u testReader:test1234 -X PUT $db/pasta_tutorial/testDocument -d '{"type":"test"}'
```
Output: {"error":"forbidden","reason":"Only Writers (W) may edit the database"}

Writer write
```bash
curl -u s.brinckmann:YYYY -X PUT $db/pasta_tutorial/testDocument -d '{"type":"test"}'
```
Output: {"ok":true,"id":"testDocument","rev":"1-3b717529ff0f515c2c5d8aa52a2c03ab"}

Anybody read
```bash
curl $db/pasta_tutorial/testDocument
```
Output: {"error":"unauthorized","reason":"You are not authorized to access this db."}

Reader read
```bash
curl -u testReader:test1234 $db/pasta_tutorial/testDocument
```
Output: {"_id":"testDocument","_rev":"1-3b717529ff0f515c2c5d8aa52a2c03ab","type":"test"}

Writer read
```bash
curl -u s.brinckmann: $db/pasta_tutorial/testDocument
```
Output: {"_id":"testDocument","_rev":"1-3b717529ff0f515c2c5d8aa52a2c03ab","type":"test"}

* * *

## Build ReactElectron
Python and the pasta-python version are required.

### Install all required packages:
```bash
git clone https://jugit.fz-juelich.de/pasta/gui.git
cd pasta_electron
npm install
```

### Allow file-watchers to see if updates occurred
```bash
sudo nano /etc/sysctl.conf
```
add at the end of file
"fs.inotify.max_user_watches=524288"

Restart system-control
```bash
sudo sysctl -p
```

## To build the program for deployment
```bash
npm build
```

* * *

## To build pasta-ReactDOM for JavaScript
This is very rarely required; only if you want to develop the PASTA framework. Note, the python branch not used for this branch.

## Install all required packages:
cd pasta_dom
```bash
npm install
```

## Start the program in testing mode
```bash
npm start
```
Under Configuration enter your credentials, that correspond to the entries in the Couchdb. For URL, leave empty as the local domain is entered as proxy in package.json.

## To build the program for deployment
```bash
npm build
```

