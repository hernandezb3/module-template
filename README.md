# Template for Creating Python Packages

This repo is a template with the folder structure below to follow along with the [Python Packaging User Guide](https://packaging.python.org/en/latest/tutorials/packaging-projects/). To get started select Use this template and Create a new repository.
```
package-template/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── package_folder/
│       ├── __init__.py
│       ├── add.py
│       └── translate.py
└── tests/
```

## Add modules
Replace add.py and translate.py with any modules to include in your package. Ensure there is an empty file called \_\_init\_\_.py in the src/package_folder/ directory with your modules.

## Customize pyproject.toml
### Build backend
The section specifying the build backend is [build-system] section of pyproject.toml. The pyproject.toml included in the template uses Setuptools for the package build backend:

```
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"
```

If you want to use a different build backend, see the [Python Packaging User Guide](https://packaging.python.org/en/latest/tutorials/packaging-projects/).

### Project info
Edit the [project] section of pyproject.toml with information specific to your package:

```
[project]
name = "package_name"
version = "0.0.1"
authors = [
    {name = "brittney hernandez", email = "author@example.com"},]
descriptiom = "what is the package for?"
readme = "README.md"
license = "MIT"
license-files = ["LICEN[CS]E*"]
```

- Replace package_name with the name of your package. This will need to be unique from other packages uploaded to [PyPI](https://pypi.org/search/)
- Determine your starting version. See [https://semver.org](https://semver.org) for more information about semantic versioning
- Add your name and email in the authors section
- Describe the package to help others on PyPI know what the package is for
- Replace this README.md with a README.md file for the project. For exmaple, see the pandas README.md for inspiration on what information to include: [https://github.com/pandas-dev/pandas](https://github.com/pandas-dev/pandas) 
- By default this template uses the MIT license but be sure to review other licenses available: [https://choosealicense.com](https://choosealicense.com)

## Rename package_folder
Rename the directory package_folder/ to match the name you specified in pyproject.toml.

## Upgrade packages
Ensure the packages  you'll use to create and upload your package (i.e., pip, build, twine) are installed and upgraded. Run the following in Terminal:
```
python3 -m pip install --upgrade pip
```
```
python3 -m pip install --upgrade build
```
```
python3 -m pip install --upgrade twine
```
## Generate distribution packages
Now run this command from the directory where pyproject.toml is located. Use cd to change your directory.
```
cd package-template
```
```
python3 -m build
```
The build command should generate two files in the dist/ directory:

```
dist/
├── package_name-version-py3-none-any.whl
└── package_name-version.tar.gz
```

## Create an account with PyPI
If you want to test a package upload, create an account with TestPyPI [https://test.pypi.org/account/register/](https://test.pypi.org/account/register/)

If you are uploading to TestPyPI you'll need to generate an API token by navigating to manage > account > api tokens
- Set “Scope” to “Entire account”
- Copy and save the token

OR if you are ready to upload a real package to PyPI create an account [https://pypi.org/](https://pypi.org/)

## Upload distribution archives
Now upload your package. Either to TestPyPI:

```
python3 -m twine upload --repository testpypi dist/*
```
You will be prompted for an API token. Use the token value, including the pypi- prefix. Note that the input will be hidden, so be sure to paste correctly. Once uploaded, your package should be viewable on TestPyPI.

OR to PyPI:

```
python3 -m twine upload dist/*
```
Enter your credentials for your PyPI account. Once uploaded your package should be viewable on PyPI.

## Test installation
Test that your package installs correctly. To install from the TestPyPI registry use:

```
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps package_name
```

OR install from PyPI:
```
python3 -m pip install package_name
```

And then load the package into a python script using:
```
import package_name
```

You can also read in specific modules -- e.g., add.py or translate.py from the src/package_folder/ directory -- using:
```
from package_name import add
```

