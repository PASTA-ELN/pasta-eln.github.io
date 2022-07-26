## Important
OUTDATED


macOS can be a bit difficult with python, if you don't have any experience with python environments on Mac use the included version 3.8 that comes with your Mac.
If PASTA is not working with your install or you have installed a newer version of Python and got stuck visit the macOS section on the [troubleshooting page](troubleshooting#macos-problems).

## To install PASTA for macOS

### Download the Pip and brew installer

1. pip:
   1. download get-pip.py
        ```bash
        curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
        ```
    2. execute the file
        ```bash
        python get-pip.py
        ```
2. brew:
    1. type in a command line:
        ```bash
        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
        ```

### Install CouchDB
1. See "Installation" and "First run" descriptions on
(https://docs.couchdb.org/en/stable/install/index.html)
While setting up, set administrator user-name and password.

2. For example for macOS Big Sur 11.0.1
    1. [Download .zip file](https://couchdb.apache.org/#download)
    2. Double click on the .zip file
    3. Drag and drop the Apache CouchDB.app into the Applications folder

3. Ensure you have a Git-identity
    ```bash
    git config -l
    ```
    If nothing there:
    ```bash
    cd ~
    ```
    ```bash
    git config --global --add user.name "Donald J Trump"
    ```
    ```bash
    git config --global --add user.email donald@example.com
    ```

### install PASTA and all dependencies
1. clone this [repository](https://github.com/PASTA-ELN/desktop)
2. open a Linux shell
3. cd into the main folder on your system
4. clone this [PythonRepository](https://github.com/PASTA-ELN/Python) as Python into the main folder
5. cd into Python folder
6. install requirements
    ```bash
    sudo pip install -r requirements.txt
    ```
7. copy ".pasta.json" into home-directory and add your account details
```
change *user* and *Password* in .pasta.json in your home directory to your CouchDB
username and password
```

### Done
Start using PASTA by "./pastaCLI.py". See [firstUsage](firstUsage)

## Unit-test in python
### Run unit test in PASTA's python folder
- run "python3 -m unittest discover -s Tests" in main folder to test installation



# Build ReactElectron

## Install all required packages:
```bash
npm install
```

## Allow file-watchers
```bash
sudo nano /etc/sysctl.conf
```
add at the end:
"fs.inotify.max_user_watches=524288"
```bash
sudo sysctl -p
```

## Start the program in testing mode
```bash
npm start
```
Credentials are extracted from the .pasta.json file (see python section) in the user directory. Here only the 'local' credentials are used.

## To build the program for deployment
```bash
npm build
```
