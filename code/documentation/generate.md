# Generate

Once you have written the docstrings for your code, you can use [Sphinx](https://www.sphinx-doc.org/en/master/) to automatically generate documentation. Sphinx ensures that your documentation is consistent, up-to-date, and easy to read, making it easier for others to understand and use your code.

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/) is a powerful tool used by the official Python documentation. It is modular and can be extended with various plugins, including:

- [autodoc](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html), the official plugin for generating API documentation from docstrings.
- [napoleon](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html), the official plugin for compatibility with Google-style docstrings.
- [sphinx-autodoc-typehints](https://pypi.org/project/sphinx-autodoc-typehints/), a plugin that detects type hints in generated documentation.

### Configuration

Refer to the [Sphinx documentation](https://www.sphinx-doc.org/en/master/) for information on how to configure Sphinx.

### Usage

To generate documentation using Sphinx, run the following command:

```sh
sphinx-build docs/ docs/_build
```

This will generate the documentation in the docs/_build directory.
