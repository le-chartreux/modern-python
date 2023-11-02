# Installation

Installing a Python project and its dependencies can be a tedious task, especially when dealing with multiple dependency groups.
However, with the `pyproject.toml` configuration file, installation can be simplified and streamlined.

## Create the virtual environment

It's not a good practice to install your Python packages system-wide, because it messes up your system, creates security risks and will certenly end up with dependencies conflicts.
Starting from Python 3.11, you will even get an error if you try to do that (`error: externally-managed-environment` from [PEP 668](https://peps.python.org/pep-0668/)).
The solution is to use a *virtual environment*, that is a self-contained and isolated workspace where you can install packages and manage dependencies separately from the system-wide Python installation.
You should use one virtual environment per project to avoid dependencies conflicts.
Let's create the one for `cleather` with [venv](https://docs.python.org/3/library/venv.html), the default creator of virtual environments of Python:

```sh
python3 -m venv .venv
```

With this command, the created environment will be named `.venv`, as recommanded in [this part](https://docs.python.org/3/tutorial/venv.html?highlight=prevents+clashing#creating-virtual-environments) of the official Python tutorial.

Next, activate it:

```sh
source .venv/bin/activate
```

You can verify that your virutal environment is correctly set using the following command:

```sh
which python3
```

That should output something ending by `/cleather/.venv/bin/python3`.

If you want exit the `venv`, you can run the following command:

```sh
deactivate
```

## Install the package

To install a project configured with a `pyproject.toml`, you can use the following command, that also installs its mandatory dependencies:

```sh
pip install .
```

You should now be able to run the `cleather` command!

```sh
$ cleather
Welcome to cleather USER!
```

Now let's try to improve this test program but putting the name of the user logged instead of `USER`.
In `__main__.py`, import the `os` module and use `os.getlogin`:

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

Sadly, the output hasn't changed!
It's because just before our installation was *static*.
If you install the package again, the output will be updated.
Howevery, it's not convenient to run a `pip` command after each modification when developing a project.
Fortunately, pip provides an editable mode, also known as development mode, that allows you to get modifications of your files instantly available.

To install the project in editable mode, you can use the following command:

```sh
pip install --editable .
```

Now, running the `cleather` command should output your username:

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
