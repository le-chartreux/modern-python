# Good Python

Small tutorial about writing a good Python code and the tools to check that it is.

A good Python code should be [tested](#test), [documented](#documentation), [type-checked](#type-check), [PEP-8 compliant](#pep-8-compilance) and [formatted](#format).

## Test

The standard testing tool for Python is [pytest](https://docs.pytest.org/en/latest/), a framework to write unit tests. To measure the code coverage (degree to which the source code of a program is executed while running its test suite), use the module [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/). [pytest](https://docs.pytest.org/en/latest/) can also run the doctests.

### Usage:

```sh
# execute unit tests
pytest
# execute unit tests with coverage mesurement
pytest --cov
# execute doctests
pytest PACKAGE_LOCATION --doctest-modules
```

## Documentation

### Write

Each public element should be documented with a [docstring](https://peps.python.org/pep-0257/). There are many docstring formats depending on the style used: [Google](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings), [Epytext](https://epydoc.sourceforge.net/manual-epytext.html), [reStructuredText](https://peps.python.org/pep-0287/), [Numpy](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard)... Choose one of them and stick to it for each project. 

Do not over comment the code: explain technical choices (name of the algorithm, design pattern used, etc.) and consequences of them (e.g. `:warning: very precise but slow, if a margin error of up to 2% is not a problem consider using XXX instead`). If you think that the content of a function needs to be commented for other reasons, consider simplifying it and using more relevant names before writing the comment.

Write examples with [doctests](https://docs.python.org/3/library/doctest.html) and execute them with [pytest](#test). Running them allows checking that the examples are still working.

#### Example with Google style

Source: [language.py by le-chartreux on hypermodern-python-tuto](https://github.com/le-chartreux/hypermodern-python-tuto/blob/master/src/hypermodern_python_tuto/wikipedia/language.py#L16).

```py
@classmethod
def from_preferences(cls) -> Self:
    """Search for the preferred language in the computer's settings.

    Since the computer settings vary a lot depending on the operating system,
    this function works on posix and Windows only.

    Returns:
        The preferred language.

    Raises:
        RuntimeError: If the os name is not posix nor Windows.

    Examples:
        >>> language = Language.from_preferences()
        >>> isinstance(language, Language)
        True
    """
    if os.name == "posix":
        return cls._from_preferences_posix()
    if os.name == "nt":
        return cls._from_preferences_windows()
    error_message = f"Unsupported operating system: {os.name}."
    raise RuntimeError(error_message)
```

### Generate

After writing the docstrings, you can use [Sphinx](https://www.sphinx-doc.org/en/master/) to generate the documentation. [Sphinx](https://www.sphinx-doc.org/en/master/) is the tool used by the official Python documentation, and it can be improved with the following plugins:
  - [autodoc](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html), official plugin to generate API documentation from the docstrings.
  - [napoleon](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html), official plugin to allow compatibility with Google-style docstrings.
  - [sphinx-autodoc-typehints](https://pypi.org/project/sphinx-autodoc-typehints/), to detect type hints in generated documentation.

Usage:

```sh
sphinx-build docs/ docs/_build
``` 

### Host

To host the [Sphinx](https://www.sphinx-doc.org/en/master/) documentation, you can use [Read the Docs](https://readthedocs.org/).

## PEP-8 compliance

## Type-check

## PEP-8 compilance

## Format

