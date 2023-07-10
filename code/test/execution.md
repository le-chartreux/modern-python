# Execution

The standard testing tool for Python is [pytest](#pytest), which has replaced [unittest](https://docs.python.org/3/library/unittest.html) as the preferred testing framework. While [pytest](https://docs.pytest.org/en/latest/) improves upon [unittest](https://docs.python.org/3/library/unittest.html), it still allows you to run [unittest](https://docs.python.org/3/library/unittest.html) tests.

## pytest

[pytest](https://docs.pytest.org/en/latest/) is a framework to write unit tests. It offers a number of advanced features such as fixtures, parametrization, and test discovery. In addition, it is modular, allowing you to improve [mocking](#mock) or mesure [coverage](#coverage) by adding plugins to meet your specific needs.

### Usage

#### Write

To write tests, follow the [pytest documentation](https://docs.pytest.org/en/latest/).

#### Execute

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

### Mock

To [mock](https://en.wikipedia.org/wiki/Mock_object) elements, you have the choice between using the traditional [unittest.mock](https://docs.python.org/3/library/unittest.mock.html) or one of its wrappers, such as [pytest-mock](https://pytest-mock.readthedocs.io/en/latest/) which brings a more pytest-like style to your mocking. 

### Coverage

If you want to measure the code coverage of your Python program (i.e., the degree to which its source code is executed while running its test suite), you can use the [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/) module. This module provides a simple and effective way to generate coverage reports for your tests.

#### Configuration

Put the following configuration in your `pyproject.toml`, with `YOUR_PACKAGE_NAME` in `[tool.coverage.run]` replaced with your package name (of course).

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
