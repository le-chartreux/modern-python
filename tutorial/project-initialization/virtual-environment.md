# Virtual environment

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

Congratulations, you are now prepared to [install](installation.md) the project!
