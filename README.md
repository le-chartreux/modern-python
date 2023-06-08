# python-dev-workflow

This is an explenation Tools of my workflow when developing in Python. It's a simplified version of my [hypermodern python tuto](https://github.com/le-chartreux/hypermodern-python-tuto) workflow.

## Tools

This part describes the tools that are used in the workflow and how to use them.

### Task runner

To run all the tasks of my workflow, I use [nox](https://nox.thea.codes/en/stable/). It allows to automate tasks and run them in multiple environments (e.g. multiple Python versions). The tasks are described in [noxfile.py](noxfile.py).

### Testing

To run unit tests and doctests, I use [pytest](https://docs.pytest.org/en/latest/), a popular framework to write unit tests. I extand it with [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/), to mesure the code coverage (degree to which the source code of a program is executed while running its test suite).

To test the code, run the following command:

```sh
# unit tests and doctests
nox -k test
# only unit tests
nox -s pytest
# only doctests
nox -s doctest
```

### Format

To format the code, two tools are used: [black](https://black.readthedocs.io/en/stable/), the main formatter, and [isort](https://pycqa.github.io/isort/index.html), to sort imports.

To format, run the following command:

```shell
nox -k format
```




