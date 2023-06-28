# Type-check

Many type-checkers are available for Python. I use the classic one, [mypy](https://mypy.readthedocs.io/en/stable/index.html), because it covers all my needs. The main other solutions are [pytype](https://github.com/google/pytype) from Google and [Pyre](https://pyre-check.org/) from Facebook. [pytype](https://github.com/google/pytype) can work without type annotations, and [Pyre](https://pyre-check.org/) is performance-oriented.

## mypy

### Usage

```sh
mypy CODE_LOCATIONS
```

### Configuration

Use `strict` to enable all optional error checking flags. Put the following configuration in your `pyproject.toml`.

```toml
[tool.mypy]
strict = true
```