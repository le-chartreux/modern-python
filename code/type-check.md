# Type-check

There are many type checkers available for Python, but I prefer to use the classic one, [mypy](https://mypy.readthedocs.io/en/stable/index.html). because it covers all my needs. Other popular solutions include [pytype](https://github.com/google/pytype) from Google and [Pyre](https://pyre-check.org/) from Facebook. While [pytype](https://github.com/google/pytype) can work without type annotations, [Pyre](https://pyre-check.org/) is performance-oriented.

## mypy

### Usage

```sh
mypy CODE_LOCATIONS
```

### Configuration

To enable all optional error checking flags, use `strict`. 
Add the following configuration to your pyproject.toml file:

```toml
[tool.mypy]
strict = true
```
