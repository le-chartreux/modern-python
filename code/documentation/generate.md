# Generate

After writing the docstrings, you can use [Sphinx](#sphinx)) to generate the documentation.

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/) is the tool used by the official Python documentation. It is modular, and can be improved with the following plugins:
  - [autodoc](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html), official plugin to generate API documentation from the docstrings.
  - [napoleon](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html), official plugin to allow compatibility with Google-style docstrings.
  - [sphinx-autodoc-typehints](https://pypi.org/project/sphinx-autodoc-typehints/), to detect type hints in generated documentation.

### Configuration

See the [Sphinx documentation](https://www.sphinx-doc.org/en/master/) for information about the configuration of Sphinx.

### Usage

```sh
sphinx-build docs/ docs/_build
``` 