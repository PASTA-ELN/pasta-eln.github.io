# Installation instructions Linux/Ubuntu
OUTDATED

## Installation script
For Windows, there is a installation script in the main folder; We suggest to download that and use it.
- download [install.bat](https://jugit.fz-juelich.de/pasta/main/-/blob/master/install.bat)
- use cmd.exe and go to download folder
- start script "install.bat"
- suggestions for [first time users](firstUsage)

Help for problems:
- General requirements and assumptions: 3GB on disk C: and a 64-bit computer
- Often a restart helps because it updates environmental variables. Restart your shell cmd.exe.
  If the script stops twice at the same point, then it is time to read the next line.
- The software is saved under "My Documents" in a subfolder. The data is at an arbitrary location. Future versions might allow more flexibility.
- If the graphical user interface (GUI) hangs:
  - "Ctrl-R" restarts it
  - "Shift-Ctrl-R" opens the Developer Tools. Go to "Console" and send everything written there to me.
- Troubleshooting are given in [hints](troubleshooting)


## Installation Guide for Windows
### 1. Download install.bat from [Main](https://jugit.fz-juelich.de/pasta/main) to "my documents"
### 2. Open Windows Powershell or cmd and enter ".\install.bat" and follow the instructions
GUI starts automatically after successfull installation.

### 3. To restart later open powershell or cmd and type
- cd c:\Users\username\Documents\pasta_source\gui
 - npm start
 (username has to be replaced!)


## Installation Guide for Windows in detail
### 1. install Python
We prefer not to use Anaconda since it uses the conda-framework making it difficult to (1) install custom packages and (2) run your own python programs from windows. It creates a bubble, which is difficult to penetrate.

Go to Python.org and download the >3.8 version of Python. Follow the installers default settings, LET INSTALLER CHANGE THE PATH VARIABLES and on the last page allow for long environment variables. Test if everything is working by starting the just installed Python IDLE and entering "2+2".

Adopt the "System Variables" or "Environment Variables" <br> (search **"systemvariables"** in the Windows search bar) and edit the variables "for your account"
Edit the entry **path** and add:
- "C:\Users\**USER**\AppData\Local\Programs\Python\Python38"
- "C:\Users\**USER**\AppData\Local\Programs\Python\Python38\Scripts"

Open a new command-shell (search for "cmd.exe") or PowerShell (search for "Powershell") and type
```bash
python.exe
```
You can exit with Ctrl-Z + Return

Install basic python packages
```bash
pip.exe install matplotlib pandas
```

Try to see if installation sucessful in python.exe prompt
```python
import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(0,2*np.pi)
y = np.sin(x)
plt.plot(x,y)
plt.show()
```

If you get a mistake that NumPy does not work... There is some issue with Windows and some basic functions. Use the cmd.exe or the PowerShell
```bash
pip install numpy==1.19.3
```

Spyder is a helpful Tool for writing python code. Install it by simply
```bash
pip install spyder
```
Then search for spyder on your hard-disk and pin it to start.

### Install Git for windows
Check if Git is already installed by typing in PowerShell:
```bash
git --version
```
If it is not installed:
1. download the latest [Git installer][git_installer_link]
2. run the executable
3. make sure **C:\Program Files\Git** is the installation path
4. under "Adjusting your PATH environment" choose: <br> **Git from the command line and also from 3rd-party software**
5. under "Choosing the ssh executable" choose: <br> **use OpenSSH**
6. under "Choosing the HTTPS transport backend" choose: <br> **Use the OpenSSL library**
7. under "Configuring the line ending conversions" choose: <br> **Checkout Windows-Style, commit Unix-Style line endings**
8. under "Configuring the terminal emulator to use with Git bash" choose: <br> **Use minTTY**
9. under "Choose the default behavior of 'git pull'" choose: <br> **Default**
10. under "Choose credential helper" choose: <br> **Git credential Manager Core**
11. under "Configure extra options" choose: <br> **Enable filesystem caching** and **Enable symbolic links**
[git_installer_link]:https://git-scm.com/download/win

### Install git-annex
Git-annex is used for the storage of large and small data files. Download the installer at
(https://downloads.kitenet.net/git-annex/windows/7/current/)

Test the installation
```bash
git-annex version
```

#### Create Git user information
Test if you have the information
```bash
git config --global -l
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

### Install CouchDB
- Go to (https://couchdb.apache.org/#download) to download the software.
- If Windows warns you, go to **more information** and **run anyway**
- Rember the user and password that you enter in the setup utility.
- go to local installation (http://localhost:5984/_utils)

Alternatively, you also find information on (https://docs.couchdb.org/en/stable/install/windows.html#installation-from-binaries), but I did not have to follow those directory requirements (aka without spaces).

### install pasta_python and all dependencies
1. Create "Python" folder in "My Documents"
2. In PowerShell, change into that folder
   ```bash
   cd Documents\Python\
   ```
3. clone repository
   ```bash
   git clone https://jugit.fz-juelich.de/s.brinckmann/pasta_python.git
   ```
   and since we are already at cloning, also clone the experimental micromechanics, which we need for testing and data processing
   ```bash
   git clone https://jugit.fz-juelich.de/s.brinckmann/experimental-micromechanics
   ```
4. change into that folder "cd pasta_python"
5. install requirements
    ```bash
    pip install -r requirements.txt
    ```
6. copy ".pasta.json" into home-directory and add your account details
```bash
cp .\.pasta.json c:\Users\**USER**\.pasta.json
```
and adopt .pasta.json in your home directory
```bash
notepad.exe c:\Users\**USER**\.pasta.json
```
- **ORCID-ID** is an arbitrary user id for your local group.
- **USER** and **PASSWORD** to your CouchDB username and password.
- **UUID** to your favorite name, e.g. pasta_tutorial
- **pasta-folder** place on your harddisk, e.g. "c:\users\**USER**\Documents\pasta"

7. Add pasta_python folder to path and python-path by editing the "System Variables" or "Environment Variables" (see above)<br>
- Edit the entry **path** and add "C:\Users\**USER**\Documents\Python\pasta_python"
- Create\Edit the entry **pythonpath** and add "C:\Users\**USER**\Documents\Python\pasta_python"

8. Run simple tests after starting a new CMD.exe (or PowerShell)
```bash
pastaDB.py test
pastaCLI.py
```
Ensure that the path to experimental-micromechanics is in your python path
open python
```python
from Tif import Tif
from nanoIndent import Indentation
```

Use the CMD.exe to change into the folder
```bash
cd C:\Users\**USER**\Documents\Python\pasta_python
python Tests\testTutorial.py
```
9. Done
Start using PASTA by "./pastaCLI.py". See [firstUsage](firstUsage)


***

# Build ReactElectron
The python branch is required for this to work.

## Install node js
Visit "https://nodejs.org/en/download/" and download the Windows version and install it. No, need to install other tools, suggested at the last screen of the installer.

## Clone Git repository
In the PowerShell, go to the "Python" folder in your "My Documents" folder.
```bash
git clone https://jugit.fz-juelich.de/pasta/gui.git
```

## Install all required packages:
You might have to open a new PowerShell because you installed a nodeJS and the PowerShell did not recognize it.
```bash
cd .\pasta_electron\
npm install
```

## Start the Graphical User Interface (GUI)
```bash
npm start
```
