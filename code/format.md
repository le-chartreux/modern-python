# Format

Having a consistent formating across your project is something very simple to automate yet that bring a lot to the lisibility of your code. I use two complementary formatters: [isort](#isort) to sort imports, and [black](#black) for the rest of the code.

## black

[black](https://black.readthedocs.io/en/stable/) is a code formatter that aims to be the standard formatting tool for Python. It is easy to use, [PEP-8](https://peps.python.org/pep-0008/) friendly (of course) and it offers minimal configuration options (that is cool because you don't want a formatter to format differently across different developers).

### Usage

```sh
# format all the Python code
black .
```

## isort

[isort](https://pycqa.github.io/isort/index.html) allows to format a part of your code left untouched by [black](#black): the order of your import statements. It splits your import list in 3 parts, as [PEP-8](https://peps.python.org/pep-0008/) recommands it: first the standard library, then the third parties, and finally your package. 

### Usage

```sh
# format all the Python code
isort .
```

### Configuration

Add the following configuration to your `pyproject.toml`. If you don't use [git](https://git-scm.com/), turn `skip_gitignore` to `false`.

```toml
[tool.isort]
profile = "black"
skip_gitignore = true
```