# Installation

Installing a Python project along with its dependencies can be a tedious task, especially when dealing with multiple dependency groups.
Thankfully, a `pyproject.toml` configuration file allows installation to be simplified and streamlined.

## Create the virtual environment

It's not a good practice to install your Python packages system-wide, as this can lead to system clutter, security vulnerabilities, and inevitable dependency conflicts.
Starting from Python 3.11, attempting to do so will result to an error (`error: externally-managed-environment`, as per [PEP 668](https://peps.python.org/pep-0668/)).
The solution is to utilize a *virtual environment*, which provides a self-contained and isolated workspace where packages can be installed and dependencies managed separately from the system-wide Python installation.

Let's create a virtual environment for cleather using [venv](https://docs.python.org/3/library/venv.html), Python's default virtual environment creator:

```sh
python3 -m venv .venv
```

The command above creates an environment named `.venv`, following the recommendation in the [official Python tutorial](https://docs.python.org/3/tutorial/venv.html?highlight=prevents+clashing#creating-virtual-environments).

Next, activate the environment with the command bellow.
Remember to **always activate the virtual environment when following this tutorial**.

```sh
source .venv/bin/activate
```

You can verify that your virtual environment is correctly set by running the following command:

```sh
which python3
```

This command should output a path ending with `/cleather/.venv/bin/python3`.

To exit the virtual environment, use the following command.

```sh
deactivate
```

## Install the package

To install a project configured with a `pyproject.toml` (along with its mandatory dependencies), use the following command:

```sh
pip install .
```

With this installation complete, you should now be able to run the `cleather` command:

```sh
$ cleather
Welcome to cleather USER!
```

Let's make a quick improvement by replacing `USER` with the logged-in user's name.
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

Congratulations, you've finished initializing your project!
To start the coding part of the project, refer to the [Chapter 2 - Code](../code/README.md).
