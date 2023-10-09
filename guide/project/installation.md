# Installation

Installing a Python project and its dependencies can be a tedious task, especially when dealing with multiple dependency groups.
However, with the `pyproject.toml` configuration file, installation can be simplified and streamlined.

To install a project configured with a `pyproject.toml`, you can use the following command:

```sh
pip install .
```

This command will install the project and all its mandatory dependencies.
It's that simple!

## Optional Dependencies

Sometimes, a project may have optional dependency groups that are not required for basic functionality.
To install an optional dependency group, you can use square brackets with the name of the group.
You can install multiple dependency groups by separating them with a comma.

For example, to install a project with the `dev` dependency group, you can use the following command:

```sh
pip install .[dev]
```

To install a project with both the `dev` and `x32` dependency groups, you can use the following command:

```sh
pip install .[dev,x32]
```

## Editable Installation

When developing a project, it's not convenient to run a `pip` command after each modification.
Fortunately, `pip` provides an editable mode, also known as development mode, that allows you to get modifications of your files instantly available.

To install a project in editable mode, you can use the following command:

```sh
pip install --editable .
```

You can also install a project in editable mode with optional dependency groups by using the following command (here with the `--editable` shorten to `-e`):

```sh
pip install -e .[dev]
```

For further information, refer to the [setuptools documentation](https://setuptools.pypa.io/en/latest/userguide/).
