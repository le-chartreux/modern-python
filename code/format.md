# Format

Maintaining consistent formatting across your project is a simple yet effective way to improve the readability of your code.
To achieve this, I use two complementary formatters: [isort](https://pycqa.github.io/isort/index.html) for sorting imports and [black](https://black.readthedocs.io/en/stable/) for the rest of the code.

## black

[black](https://black.readthedocs.io/en/stable/) is a code formatter that aims to be the standard formatting tool for Python.
It has many advantages:

- Ease of [use](#usage).
- [PEP 8](https://pep8.org/) compliance (of course).
- Minimalistic configuration, which ensures that the formatting stays consistent across different developers.
- Deterministic (it always produces the same output), so it can be used on [CI/CD](https://en.wikipedia.org/wiki/CI/CD) pipelines.

### Usage

```sh
# format all the Python files of your project
black .
```

## isort

[isort](https://pycqa.github.io/isort/index.html) is a tool that formats a part of your code left untouched by [black](https://black.readthedocs.io/en/stable/): the order of your import statements.
It splits your import list into 3 parts, as recommended by [PEP-8](https://pep8.org/): first the standard library, then the third-party modules, and finally your own package.

### Usage

```sh
# order all the imports of your Python files
isort .
```

### Configuration

Add the following configuration to your `pyproject.toml`.
If you don't use [git](https://git-scm.com/), turn `skip_gitignore` to `false`.

```toml
[tool.isort]
profile = "black"
skip_gitignore = true
```
