**THIS METHOD IS NOT RECOMMENDED ANYMORE AND KEPT HERE FOR REFERENCE**
it results in a slow, unusable result

# To install PASTA database for Python
### Download WSL for windows
 1. open a PowerShell prompt and activate WSL
    ```bash
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```
    then restart when asked
 2. open the [Microsoft Store](https://aka.ms/wslstore) and download a Linux version
 3. run the Linux Version from windows start menu
 4. set up your Linux account as usual

### install git for windows

1. download the latest [Git installer](https://git-scm.com/download/win)
2. run the executable
3. make sure **C:\Program Files\Git** is the installation path
4. under "Adjusting your PATH enviroment" choose: <br> **Git from the command line and also from 3rd-party software**
5. under "Choosing the ssh executable" choose: <br> **use OpenSSH**
6. under "Choosing the HTTPS transport backend" choose: <br> **Use the OpenSSL library**
7. under "Configuring the line ending conversions" choose: <br> **Checkout Windows-Style, commit Unix-Style line endings**
8. under "Configuring the terminal emulator to use with Git bash" choose: <br> **Use minTTY**
9. under "Choose the default behavior of 'git pull'" choose: <br> **Default**
10. under "Choose credential helper" choose: <br> **Git credential Manager Core**
11. under "Configure extra options" choose: <br> **Enable file system caching** and **Enable symbolic links**

### install all dependencies
1. clone this [repository](https://jugit.fz-juelich.de/s.brinckmann/pasta_python.git)
2. open a Linux shell
3. cd into the repository folder on your system#
4. install requirements
    ```bash
    sudo pip install -r requirements.txt
    ```
### Install couchDB
1. See "Installation" and "First run" descriptions on
(https://docs.couchdb.org/en/stable/install/index.html)
While setting up, set administrator user-name and password.

2. For example for Ubuntu 20.04:
    ```bash
    sudo apt-get install -y gnupg ca-certificates
    echo "deb https://apache.bintray.com/couchdb-deb focal main" | sudo tee /etc/apt/sources.list.d/couchdb.list
    ```
    ```bash
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8756C4F765C9AC3CB6B85D62379CE192D401AB61
    ```
    ```bash
    sudo apt update
    ```
    ```bash
    sudo apt install -y couchdb
    ```

3. Ensure you have a git-identity
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

### install PASTA database for python
Finally install from [this git-repository](https://jugit.fz-juelich.de/s.brinckmann/pasta_python.git)
- clone this directory from git-repository
- copy ".pasta.json" into home-directory and add your account details
```
change *user* and *Password* in .pasta.json in your home directory to your CouchDB
username and password
```

- unit test requires additional libraries for Tifs, Nanoindentation. (see below)
### Done
Start using PASTA by "./pastaCLI.py". See [firstUsage](firstUsage)

## Unit-test in python
### Install dependencies for some of the tested data
use git to install:
https://jugit.fz-juelich.de/s.brinckmann/experimental-micromechanics

### Ensure that the path to experimental-micromechanics is in your python path
open python
```python
from Tif import Tif
from nanoIndent import Indentation
```

### Run unit test in PASTA's python folder
- run "python3 -m unittest discover -s Tests" in main folder to test installation


***
# To build PASTA-ReactDOM for javascript
python branch not used for this branch

## Install all required packages:
goto ./pasta_dom
```bash
npm install
```

## Start the program in testing mode
goto ./pasta_dom
```bash
npm start
```
Under About/Configuration enter your credentials, that correspond to the entries in the couchdb. For url, leave empty as the local domain is entered as proxy in package.json. Example credentials: {"user":"my_user_name", "password":"qwerty", "url":"","database":"database_name"}

## To build the program for deployment
goto ./pasta_dom
```bash
npm build
```

***

# Build ReactElectron
python branch is right now not used for this branch. This will change in the future.

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
