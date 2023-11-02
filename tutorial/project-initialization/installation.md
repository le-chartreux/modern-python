# Installation

Installing a Python project along with its dependencies can be a tedious task, especially when dealing with multiple dependency groups.
Thankfully, a `pyproject.toml` configuration file allows installation to be simplified and streamlined.

To install a project configured with a `pyproject.toml` (along with its mandatory dependencies), use the following command:

```sh
pip install .
```

With this installation complete, you should now be able to run the `cleather` command:

```sh
$ cleather
Welcome to cleather USER!
```

Congratulations, it works!
However, before you celebrate too quickly, there's a small problem to solve.

To bring the problem to light, let's make a quick improvement by replacing `USER` with the logged-in user's name.
In the `__main__.py` file, import the `os` module and use `os.getlogin` as follows:

```python
"""Executable of cleather."""

import os

from cleather import create_welcome_message


def main() -> None:
    """Welcome the user with its system name."""
    welcome_message = create_welcome_message(os.getlogin())
    print(welcome_message)
```

Now, run the `cleather` command again:

```sh
$ cleather
Welcome to cleather USER!
```

Unfortunately, the output hasn't changed!
This is because our initial installation was *static*.
If you were to install the package again, the output would reflect your code changes.
However, it's not convenient to run a `pip` command after every modification during project development.
Fortunately, pip provides an editable mode, also known as development mode, which enables you to see your file modifications instantly.

To install the project in editable mode, execute the following command:

```sh
pip install --editable .
```

Now, running the `cleather` command should display your username:

```sh
$ cleather                
Welcome to cleather le-chartreux!
```

And modifing the code of your project doesn't requires to re-run the `pip install` command.
To check it, add another line to your `__main__.py`:

```python
"""Executable of cleather."""

import os

from cleather import create_welcome_message


def main() -> None:
    """Welcome the user with its system name."""
    welcome_message = create_welcome_message(os.getlogin())
    print(welcome_message)
    print("Nice username :)")
```

When running the `cleather` command again, the output should be updated:

```sh
$ cleather
Welcome to cleather le-chartreux!
Nice username :)
```

Congratulations on the successful installation of your project!
To complete this chapter, all that's left is some file [cleaning](cleaning.md) of the files created to test the installation.
