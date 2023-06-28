# Tools

The standard testing tool for Python is [pytest](#pytest). It was previously [unittest](https://docs.python.org/3/library/unittest.html), but [pytest](https://docs.pytest.org/en/latest/) improves it while still allowing to run [unittest](https://docs.python.org/3/library/unittest.html) tests.

## pytest

[pytest](https://docs.pytest.org/en/latest/) is a framework to write unit tests. It is modular: to measure the code coverage (degree to which the source code of a program is executed while running its test suite), use the module [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/).
[pytest](https://docs.pytest.org/en/latest/) can also run the doctests.

To [mock](https://en.wikipedia.org/wiki/Mock_object) elements, you can either use the traditional [unittest.mock](https://docs.python.org/3/library/unittest.mock.html), or one of its wrappers like [pytest-mock](https://pytest-mock.readthedocs.io/en/latest/) to bring a more pytestic style to your mocking. 

## Usage

```sh
# execute unit tests of the project
pytest
# execute a specific file
pytest tests/path/test_something.py
# execute unit tests with coverage mesurement
pytest --cov
# execute doctests (specify src/ to avoid running unit tests)
pytest src/ --doctest-modules
```

## Configuration

Put the following configuration in your `pyproject.toml`.

```toml
[tool.coverage.paths]
source = ["src"]

[tool.coverage.run]
branch = true
source = ["YOUR_PACKAGE_NAME"]

[tool.coverage.report]
show_missing = true
fail_under = 100
```
