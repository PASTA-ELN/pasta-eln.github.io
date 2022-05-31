# Installation instructions Linux/Ubuntu
## Installation script
For Ubuntu 20.04, there are installation script in the main folder. We strongly recommend to use it.
- download [install.sh](https://jugit.fz-juelich.de/pasta/main/-/blob/master/install.sh)
- use terminal to change into folder, e.g. "cd ~/Downloads"
- "chmod 755 install.sh"
- "sudo ./install.sh | tee installPASTA.log"
- suggestions for [first time users](firstUsage)

Help if problems occur:
- 'conda' makes things complicated, it is deactivated temporarily during the install script
- If the install does not finish: send me the files "installPASTA.log", "installPASTA2.log"
- If the graphical user interface (GUI) hangs:
  - "Ctrl-R" restarts it
  - "Shift-Ctrl-R" opens the Developer Tools. Go to "Console" and send everything to me.
- General requirements and assumptions: 3GB and a 64-bit computer
- Troubleshooting [hints](troubleshooting) are given



## Manual installation instructions
### Prepare python by installing dependencies
Ensure and python's OpenCV is installed
```bash
sudo apt-get install -y python3-opencv
```
Ensure that 'datalad' is installed. If that fails, checkout (http://neuro.debian.net/install_pkg.html?p=datalad)

Use the following to install all python requirements
```bash
sudo -H pip3 install -r requirements.txt
```

Ensure Pillow-image is working: command 'xv' has to exist
```bash
sudo ln -s /usr/bin/gpicview /usr/bin/xv
```

### Install CouchDB
See "Installation" and "First run" descriptions on
(https://docs.couchdb.org/en/stable/install/index.html)
While setting up, set administrator user-name and password.

For example for Ubuntu 20.04:
```bash
sudo apt update && sudo apt install -y curl apt-transport-https gnupg
curl https://couchdb.apache.org/repo/keys.asc | gpg --dearmor | sudo tee /usr/share/keyrings/couchdb-archive-keyring.gpg >/dev/null 2>&1
source /etc/os-release
echo "deb [signed-by=/usr/share/keyrings/couchdb-archive-keyring.gpg] https://apache.jfrog.io/artifactory/couchdb-deb/ ${VERSION_CODENAME} main" | sudo tee /etc/apt/sources.list.d/couchdb.list >/dev/null
sudo apt update
sudo apt install -y couchdb
```

### Ensure you have a Git-identity
Test git-identity
```bash
git config -l
```
If nothing there:
```bash
cd ~
git config --global --add user.name "Donald J Trump"
git config --global --add user.email donald@example.com
```

### install PASTA for python
Install python backend and frontend
- clone this directory from Git-repository
- copy ".pasta.json" into the home-directory and add your account details
```
change *user* and *Password* in .pasta.json in your home directory to your CouchDB
username and password
```

### Build ReactElectron
Python and the pasta-python version are required.

#### Install all required packages:
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

### Start the program in testing mode
```bash
npm start
```
