## What to do if problems occur?
Table of contents
- [Problems during installation](#problems-during-installation)
- [Problems after installation](#problems-after-installation)

<br />
- - -
<br />

### Problems during installation
#### Rerun installation script
- Rerun the script will solve issues related to a temporary internet stoppage
#### General procedure if rerun does not work
- check if PASTA-source directory exists with content and has a Python folder in it
- change into that Python folder
- "pip install -r requirements.txt" with a preceding sudo on Linux
- "pastaELN.py test"
- "python Tests/verifyInstallation.py"
#### Last resort
- copy the entire output/input in the terminal/command window
- remove password and username (both somewhat in the middle)
- email this information to developer

<br />
- - -
<br />

### Problems after installation
#### Verify backend functionality
PASTA has some build-in self-tests and self-repair functionality. It is not automatically executed since it is time-consuming. In the given order, execute the commands on the terminal. If a problem occurs, copy-paste the text-output of the last step (the unsuccessfull) and send it to Steffen for identification.

1. Update PASTA and its parts
   - Windows: 'cd' into the main and GUI directory and git pull
     - 'cd pasta_source/main'
     - 'git pull'
     - 'cd ../gui'
     - 'git pull'
3. 'pastaDB.py test'  (old versions) 'pastaELN.py test' (future versions)
   - Does it produce "SUCCESS" in line 2 and at the end? If not:


#### Problems with graphical user interface (GUI)
- Go to config-page: three horizontal bars on top-left corner
- Click "HEALTH" check. If that does not help, and if those suggestions do to solve the issue...

##### How can I get more information?

- use "Ctrl-Shift-I" on the keyboard (or use the "Alt"-Button to open the Menu and then View->Toggle Developer Tools)
- go to the "Console" tab
- copy-paste everything in there (there should not be any passwords) and send that information to the developer by email

<br />
- - -
<br />

### Problems with backend / Advanced troubleshooting
#### Basic tests if something is not working in shell
You can run some basic tests to see if the installation is working by using a shell and executing:
- "pastaELN.py test"
- "pastaELN.py checkDB"

##### If "pastaDB.py test" fails with an authorization error
1. use a webbrowser and go to http://127.0.0.1:5984/_utils
  - test if you remember the username and password
2. .pastaELN.json in home folder (Windows c:/user/**yourName**) with an editor
  - edit entries after "user" and "password"
  - "-userID" does not matter.
  - Entries under "remote" do not matter, either.

#### Test couchDB server (done automatically during pastaDB test)
Test if server is alive
```bash
curl http://127.0.0.1:5984
```
Log into couchDB server at least once, (2) run test, (3) setup as "single node"


#### Problems with configurations (softwareDir does not exist, ...)
- Run in the shell the command "pastaDB.py checkConfiguration" to test it
- To repair configuration "pastaDB.py checkConfigurationDev"

<br />
- - -
<br />

### General issues
#### What to do if a measurement is not automatically included upon scan
- run "pastaDB.py extractorTest filepath_from_pasta_base"
- check excluded in .gitignore
- check if already in DataLad. Go into project folder and "datalad status"
  then "datalad unlock *file*"
- try scan again


#### If you change the project-layout and delete steps and tasks
- content moved to a folder with the name 'trash_'
- check if empty: only .id_pasta.json
- if it is empty then delete
- one could do that automatically: but currently not done for safety


#### Error: cannot load module...
It is pausible that you use 'conda' and that screws up things. Use 'conda deactivate' to deactivate it in this window. Then you can test things, run the python scripts of this pastaDB.

