# Creating a Python Package

* [Requirements](#requirements)
* [Setup](#setup-your-package)
* [Uploading](#upload-your-package)
* [Links](#links)

# Requirements
Make sure you have the latest versions of `setuptools`, `wheel` and `twine` installed:
```
pip3 install --upgrade setuptools
pip3 install --upgrade wheel
pip3 install --upgrade twine
```

# Setup your package
Make sure your module contains docstrings for every function, and for the module itself. This is very useful for many reasons as we will see later – after all people need to know how to use your Python module.

Create a directory for your package which will contain the following files:
```
mypackage/
  README.txt
  LICENSE
  setup.py
  mymodule/
    __init__.py
```

Name your module `__init__.py` within the `mymodule` directory.

Create a `README.txt` file containing a summary of what your Python package is all about.

Choose a `LICENSE` for your module.

Create a `setup.py` file. This is a script that is used to compile your package and submit it to PyPI. Here is an example:
```python
import setuptools

classifiers=[
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

setuptools.setup(
    name='mypackage',
    version='1.0.0',
    description="A short description",
    long_description=open("README.md", "r").read(),
    long_description_content_type="text/markdown",
    url="https://github.com/Noxmain/NoxmainNetwork",
    author="Noxmain",
    author_email="noah.finalcut@gmail.com",
    license='MIT',
    classifiers=classifiers,
    packages=setuptools.find_packages(),
    install_requires=['']
)
```
For the list of classifiers that you can use, see https://pypi.python.org/pypi?%3Aaction=list_classifiers. Use as many as you think is relevant to your package.

We are nearly finished now. This is probably a good point to place your package in source code control on something like GitHub or similar.

# Upload your package
The next step is to generate distribution packages for the package. These are archives that are uploaded to the Package Index and can be installed by pip. To do so, run this command from the same directory where setup.py is located:
```
python3 setup.py sdist bdist_wheel
```

This command should output a lot of text and once completed should generate two files in the dist directory:
```
dist/
  mypackage-1.0.0-py3-none-any.whl
  mypackage-1.0.0.tar.gz
```

The .tar.gz file is a Source Archive whereas the .whl file is a Built Distribution. Newer pip versions preferentially install built distributions, but will fall back to source archives if needed. You should always upload a source archive and provide built archives for the platforms your project is compatible with. In this case, our example package is compatible with Python on any platform so only one built distribution is needed.

After generating your distributiuon packages, use this command and enter the credentials for your PyPI account to upload your package.
```
twine upload dist/*
```

Install your package from PyPI using this command:
```
pip3 install mypackage
```

# Links
* https://www.wyre-it.co.uk/blog/creating-a-python-package/
* https://packaging.python.org/tutorials/packaging-projects/
