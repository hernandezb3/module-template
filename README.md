# Template for Creating Python Modules

This repo is a template with the folder structure below to follow along with the [Python Packaging User Guide](https://packaging.python.org/en/latest/tutorials/packaging-projects/). To get started select Use this template and Create a new repository.
```
module-template/
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

## Ensure pip is upgraded
```
python3 -m pip install --upgrade pip
```

## Add own modules
Replace add.py and translate.py with any modules to include in your package.

Ensure there is an empty file called __init__.py in the src folder with your modules.

## Customize pyproject.toml
### Build backend
The file pyproject.toml included here uses Setuptools for the package build backend. The section specifying the build backend is:

```
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"
```

### Customize project info
Edit the project information in pyproject.toml:

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
- Replace this README.md with a README.md file for the project. For exmaple, see the pandas README.md to see what information might be helpful to include: [https://github.com/pandas-dev/pandas](https://github.com/pandas-dev/pandas) 
- By default this template uses the MIT license but be sure to review other licenses available: [https://choosealicense.com](https://choosealicense.com)

## Name package_folder
Rename the directory package_folder to match the name of your package. Ideally this also matches the name of the repository.


## Generate distribution packages
Upgrade build
```
python3 -m pip install --upgrade build
```

Now run this command from the same directory where pyproject.toml is located:

```
python3 -m build
```

The command should generate two files in the dist directory:

```
dist/
├── package_name-version-py3-none-any.whl
└── package_name-version.tar.gz
```

## Create an account with PyPI
To register with TestPyPI repository which is for testing package uploads use [https://test.pypi.org/account/register/](https://test.pypi.org/account/register/)

If you are uploading to TestPyPI you'll need to generate an API token by navigating to manage > account > api tokens
- Set “Scope” to “Entire account”
- Copy and save the token

OR if you are ready to upload a real package to PyPI register with [https://pypi.org/](https://pypi.org/)

## Upload distribution archives
Now upload your package to Python Package Index

Ensure twine is up-to-date
```
python3 -m pip install --upgrade twine
```

And then upload your package to either the test repository:
```
python3 -m twine upload --repository testpypi dist/*
```

OR the PyPI repository:
```
python3 -m twine upload dist/*
```
You will be prompted for an API token. Use the token value, including the pypi- prefix. Note that the input will be hidden, so be sure to paste correctly.

Once uploaded, your package should be viewable on TestPyPI.