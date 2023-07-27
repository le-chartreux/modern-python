# Type-check

Python offers several type checkers, but one of the most popular and widely used is [mypy](https://mypy.readthedocs.io/en/stable/index.html). It is a classic type checker that covers all the basic needs of a developer. Other popular solutions include [pytype](https://github.com/google/pytype) from Google and [Pyre](https://pyre-check.org/) from Facebook. While [pytype](https://github.com/google/pytype) can work without type annotations, [Pyre](https://pyre-check.org/) is performance-oriented. Because it covers all my needs, I only use [mypy](#mypy).

## mypy

### Usage

To use mypy, simply run the following command:

```sh
mypy CODE_LOCATIONS
```

### Configuration

To enable all optional error checking flags in mypy, you can add the following configuration to your `pyproject.toml` file:

```toml
[tool.mypy]
strict = true
```

Enabling `strict` will allow mypy to catch more potential issues in your code, helping you write more robust and error-free Python code.
