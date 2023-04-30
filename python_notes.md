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
