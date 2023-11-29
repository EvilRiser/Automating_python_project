# Automating_python_project
___

## Step 1:  
## Setup/ restructure project
___
This Part:
- separate src and tests
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

<b>file</b>:pyproject.toml
```
[build-system]
requires = ["setuptools>=42.0", "wheel"]
build-backend = "setuptools.build_meta"
```

2. setup.py  
 You can run arbitrary code inside your setup.py file since it is a python script.
And this is seen increasingly as a security risk. and so more and more code is stripped out of setup.py 
file and put into these other configuration files

<b>file</b>:setup.py
```python
from setuptools import setup

if __name__ == "__main__":
    setup()
```
even though this file is empty it will help us to install our package
in editable mode.  

3. setup.cfg  
Now all the metadata of my project like the title and description goes in the setup.cfg file.  
since this is just a configuration file and not a python script, no need to worry about executing
arbitrary code.

<b>file</b>:setup.cfg
```
[metadata]
name = slapping
description = slap that like button
author = Shaurabh Saha
license = MIT
license_file = LICENSE
platforms = unix, linux, osx, cygwin, win32
classifiers =
    Programming Language :: Python :: 3
    Programming Language :: Python :: 3 :: Only
    Programming Language :: Python :: 3.6
    Programming Language :: Python :: 3.7
    Programming Language :: Python :: 3.8
    Programming Language :: Python :: 3.9

[options]
packages =
    slapping
install_requires =
    requests>=2
python_requires = >=3.6
package_dir =
    =src
zip_safe = no
```
4. requirements.txt  
It has all my dependencies
```
requests==2.26.0
```

Now eveything is done. Just write
```Shell
$ pip install -e .
```
It will install all dependencies and slapping library in editable mode.
i.e. it just puts a link in the virtual environment, we don't need to install
it everytime we make some changes.
___
## Step 2:
Creating another requirements file which has just development requirements  

<b>file</b>:requirements_dev.txt
```
flake8==3.9.2
tox==3.24.3
pytest==6.2.5
pytest-cov==2.12.1
mypy===0.910
```
Similarly updating the setup.cfg file  

<b>file</b>:setup.cfg
```
[options.extras_require]
testing =
    pytest>=6.0
    pytest-cov>=2.0
    mypy>=0.910
    flake8>=3.9
    tox>=3.24
```
Add below section in setup.cfg file to indicate that the python 
package has been type hinted  

<b>file</b>:setup.cfg
```
[options.package_data]
slapping = py.typed
```
Add another blank file "py.typed" in slapping folder right next to init file of slapping package

Then we are adding one more line in config file for the flake8 program that we're going to be using
  
<b>file</b>:setup.cfg
```
[flake8]
max-line-length = 160
```


## Using 
Nowadays, the community is moving more and more configurations to toml file and just keeping the metadata
in the setup.cfg file, it depends on program to program

And now add all the configurations to toml file 
## 1. pytest(tests)

[pyproject.toml]
```
[tool.pytest.ini_options]
addopts = "--cov=slapping"
testpaths = [
    "tests",
]
```
## 2. mypy(checking type hints)

[pyproject.toml]
```
[tool.mypy]
mypy_path = "src"
check_untyped_defs = true
disallow_any_generics = true
ignore_missing_imports = true
no_implicit_optional = true
show_error_codes = true
strict_equality = true
warn_redundant_casts = true
warn_return_any = true
warn_unreachable = true
warn_unused_configs = true
no_implicit_reexport = true
```
## 3. flake8(for linting or checking code style)
___
## Step 3:
## Multiple envs with tox
___
## Step 4:
## Github actions
___