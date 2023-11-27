# Automating_python_project
___

## Step 1:  
## Setup/ restructure project
___
This Part:
- separate src an tests
- turn project into an installable package

Structure of file:  
(To generate write- $ tree /f > tree.txt)
```Shell
│   README.md
│   tree.txt
│   
├───src
│   └───slapping
│           slap_that_like_button.py
│           __init__.py
│           
└───tests
        conftest.py
        test_slapping.py
        __init__.py
```
1. pyproject.toml  
Earlier there was only one way to install packages, you needed the setup.py files
But nowadays, there are many other alternatives like poetry or flit.
Or still you can use setup tools.

pyproject.toml just tells us that we are using the old  way.

[pyproject.tox]
```
[build-system]
requires = ["setuptools>=42.0", "wheel"]
build-backend = "setuptools.build_meta"
```

2. setup.py  
 You can run arbitrary code inside your setup.py file since it is a python script.
And this is seen increasingly as a security risk. and so more and more code is stripped out of setup.py 
file and put into these other configuration files

[setup.py]
```python
from setuptools import setup

if __name__ == "__main__":
    setup()
```
even though this file is empty it will help us to install our package
in editable mode.
3. setup.cfg  
Now all the metadata of my project like the title and description goes in the setup.cfg file.  
since this is just 
___
## Step 2:
## Using 
## 1. pytest(tests)
## 2. mypy(checking type hints)
## 3. flake8(for linting or checking code style)
___
## Step 3:
## Multiple envs with tox
___
## Step 4:
## Github actions
___