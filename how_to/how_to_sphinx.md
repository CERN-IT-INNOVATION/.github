# Sphinx Tutorial

How to build automatic project documentation with Sphinx ([Sphinx-docs](https://www.sphinx-doc.org/en/master/)).  
The procedure detailed in this tutorial summarizes the instructions explained
[here](https://hplgit.github.io/teamods/sphinx_api/html/sphinx_api.html).

Please, use one of the following two standards:
[Google's docstring](https://google.github.io/styleguide/pyguide.html) or
[Numpy's docstring](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard).

## Useful links

The following list collects all the useful links to learn how to properly
document Python projects

- [Simple Formatting Rules](https://hplgit.github.io/teamods/sphinx_api/html/sphinx_api.html)
- [A ReStructuredText Primer](https://docutils.sourceforge.io/docs/user/rst/quickstart.html)
- [Example NumPy Style Python Docstrings](https://www.sphinx-doc.org/en/master/usage/extensions/example_numpy.html#example-numpy)
- [NumPy Style Python Docstrings Guide](https://numpydoc.readthedocs.io/en/latest/format.html#documenting-classes)
- [Example Google Style Python Docstrings](https://www.sphinx-doc.org/en/master/usage/extensions/example_google.html#example-google)
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Read the Docs tutorial](https://docs.readthedocs.io/en/stable/tutorial/)

## Project directory structure

Let's assume that the directory structure is the following:

```text
root
|-- docs
|-- src
    |-- project-name
        |-- module1.py
        |-- module2.py
```

Namely, the `root` folder contains:

- `src/project-name`: the project directory with two modules.
- `docs`: the documentation directory, that will host the Sphinx documentation.

## Quick-start Sphinx

`cd` into the documentation directory and let Sphinx create automatically the
needed files:

```bash
cd docs
sphinx-quickstart
```

And follow the steps. The output of this procedure should look like the following:

```text
Welcome to the Sphinx 4.5.0 quickstart utility.

Please enter values for the following settings (just press Enter to
accept a default value, if one is given in brackets).

Selected root path: .

You have two options for placing the build directory for Sphinx output.
Either, you use a directory "_build" within the root path, or you separate
"source" and "build" directories within the root path.
> Separate source and build directories (y/n) [n]: y

The project name will occur in several places in the built documentation.
> Project name: PyMandelbrot
> Author name(s): Marco Rossi
> Project release []: 1.0.0

If the documents are to be written in a language other than English,
you can select a language here by its language code. Sphinx will then
translate text that it generates into that language.

For a list of supported codes, see
https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
> Project language [en]: 

Creating file .../docs/source/conf.py.
Creating file .../docs/source/index.rst.
Creating file .../docs/Makefile.
Creating file .../docs/make.bat.
```

It is always recommended to keep the `source` and `build` directories distinct.

## Edit the configuration file

The `docs/source/conf.py` file describes Sphinx settings and options.  
A lot of features can be customized from this file. The following list contains
the minimal example.  
Refer to [sphinx-doc](https://www.sphinx-doc.org/en/master/usage/configuration.html)
for the full list of options.

- path setup:

  Uncomment the following lines to let Sphinx discover the package source folder

  ```python
  # import os
  # import sys

  # sys.path.insert(0, os.path.abspath(".."))
  ```

  If the package has the folder structure described above, the following lines
  can be used instead.  

  ```python
  import os
  import sys

  sys.path.insert(0, os.path.abspath("../../src/"))
  ```

- extensions:

  Add the necessary extensions to allow `autodoc` produce the automatic package
  documentation:

  ```python
  extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.viewcode',
    'sphinxcontrib.napoleon',
  ]
  ```

  `napoleon` is an useful extension to pre-process docstrings, following
  Google's or NumPy's standard, into the Sphinx desired format.
  Maybe some libraries are not present in your env so you can install those via ```pip```, i.e.:
  ```pip install sphinxcontrib-napoleon``` or ```pip install sphinx_rtd_theme```
  According to the package versioning you should use ```sphinx.ext.napoleon``` instead of ```sphinxcontrib.napoleon``` in your conf.py
  
- theme:

  The nice [Read the Docs](https://readthedocs.org/) theme can be enabled setting
  the `html_theme` variable, like the following:

  ```python
  html_theme = 'sphinx_rtd_theme'
  ```

- static paths:

  The `html_static_path` is usually not needed. The beginner user can comment out this variable:

  ```python
  # html_static_path = ['_static']
  ```

- source links:

  An hyperlink to the relevant source code is added next to each documented
  function if this variable is set to `True`:

  ```python
  html_show_sourcelink = True
  ```

## Let `autodoc` discover the package modules

Sphinx can now build the documentation running the `make html` command from the
`docs` folder.  
However, `autodoc` is not aware of the (sub)packages contained in the source code
and should be instructed about that.

### Manual module discovery

Suppose that the package `pkg` contains two modules
`mod1.py` and `mod2.py`, to be included in the documentation. Then the user must
create a file `pkg.rst` containing the following code:

```rst
pkg package
============

pkg.mod1 module
-------------------

.. automodule:: pkg.mod1
   :members:
   :undoc-members:
   :show-inheritance:

pkg.mod2 module
-------------------

.. automodule:: pkg.mod2
   :members:
   :undoc-members:
   :show-inheritance:
```

Finally, the file `pkg.rst` must be properly linked into the `index.rst` file,
to be reached in the html output.

### Automatic module discovery

The number of modules in a package can easily grow large, especially for big
projects. Therefore, is useful to have an automatic tool that correctly links the
modules within the package (and between the sub-packages).

The `sphinx-apidoc` builds automatically the API documentation, avoiding the
manual procedure just described.  
Run the following command from the `docs` directory:

```bash
sphinx-apidoc -f -o source ../src/<project-name>
```

This will produce the relevant files in the documentation.

## Build the docs

As already anticipated, the docs can be build from the `docs` folder, with the
`make html` command. The documentation will be created into the `docs/build`
folder.

Alternative output formats can be produced, simply changing the target of `make`.  
To discover all the available formats, just run `make` and a list of choices will
appear.

## Readthedocs integration

The procedure described above builds the documentation locally and might be
useful for inspecting it privately.  
Once the project becomes public, however, it is desirable to publish online the
docs to teach other users and contributors how to use the code.  
[readthedocs.org](https://readthedocs.org/) hosts online a platform for such
purpose.

Follow this [tutorial](https://docs.readthedocs.io/en/stable/tutorial/) to
import GitHub repositories to Read the Docs.

### GitHub - Read the Docs Integration

Refer to this [link](https://docs.readthedocs.io/en/latest/integrations.html) for
connecting Read the Docs to GitHubs via *webhooks*.
