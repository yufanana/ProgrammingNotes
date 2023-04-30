# Python

Author: __*yufanana*__

</br>
____

## Virtual Environments
Allows different package versions to be used for different projects. <br>
e.g. numpy 1.21.5 for project 1, and numpy. 1.18 for project 2 <br>

Install `venv`, <br>
`python3 -m pip install --user virtualenv`

**Create** venv in current directory <br>
`python -m venv project_env` <br>
Python version used to create venv will be the venv python version.

**Activate** venv <br>
Windows: `project_env\Scripts\activate.bat` <br>
Mac/Unix: `source project_env/bin/activate`

**Deactivate** venv <br>
Windows: `deactivate` <br>

**Delete** venv by removing its directory <br>

*requirements.txt* file to contain all the package versions needed for your project. <br>
`pip freeze` to generate the package versions formatted for *requirements.txt* <br>
`pip install -r requirements.txt` to install all the packages listed inside the file.
# Python Notes

Author: __*yufanana*__
____

## Setup

- Download Python from https://www.python.org/downloads/
- Select option to "Add Python to PATH"

This creates a system-wide/global Python install.

*Path is used to contained executables from the command line without having the need to specify the location*


## Virtual Environments

Instructions from [here](https://mothergeo-py.readthedocs.io/en/latest/development/how-to/venv-win.html)

`python -m venv my-venv` 
Creates a virtual environment called `my-venv` in the current directory

`.\my-venv\scripts\activate`
Activates the venv on Windows

`source my-venv/bin/activate`
Activates the venv on Linux

`pip freeze > requirements.txt`
Creates a file that enumerates the installed packages

`pip install -r requirements.txt`
Installs the packages listed in `requirements.txt`

`deactivate`
Returns to normal system settings

`rm -r my-venv`
Removes/deletes the deactivated venv

## Virtual Environment Wrapper
`pip install virtualenvwrapper-win`
Installs the wrapper for Windows

`mkvirtualenv my-venv` 
Creates a virtual environment called `my-venv` in a centralised directory, and activates the venv

`deactivate`
Returns to normal system settings

`mkvirtualenv my-venv` 
Creates a virtual environment called `my-venv`

`workon`
Lists the venv made using the mk wrapper

`workon my-venv`
Activates the venv, or jump from the current venv to the specifed venv

`rmvirtualenv my-venv`
Removes/deletes the deactivated venv

`rmvirtualenv my-venv`
Removes/deletes the deactivated venv