# Installation

It's very easy to install a project configured with a `pyproject.toml`: you just have use the following command.
The project and its dependencies with be installed.

```sh
# standard project
pip install .
```

## Optional dependencies

If you want to install an optional dependency group too, use square braquets with the name of the group.
You can install multiple dependency groups by separating them with a comma.

```sh
# with dependency group 'dev'
pip install .[dev]
# with dependency group 'dev' and 'x32'
pip install .[dev,x32]
```

## Editable installation

If you want to develop on the project, it's not convinient to run a `pip` command after each modification.
Hopefully, `pip` provides an editable mode, that will allow you to get modifications of your files instantly available.
For further information, refer to the [setuptools documentation](https://setuptools.pypa.io/en/latest/userguide/development_mode.html).

```sh
# editable mode (aka development mode)
pip install --editable . 
```
