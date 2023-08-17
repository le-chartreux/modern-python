# Local

[Nox](https://nox.thea.codes/en/stable/)
To run actions locally, my favorite tool is [tox](https://tox.wiki/).

## Tox

You can see [tox](https://tox.wiki/) as a [make](https://www.gnu.org/software/make/manual/make.html) specialized for Python, that allows you to use virtual environments and run actions across multiple Python versions.

### Usage

### Configuration

```ini
[tox]
env_list =
    pytest,
    ruff,
    mypy

labels =
    test = pytest
    lint = ruff
    typecheck = mypy
    format = black, isort
    clean = pyclean

[testenv]
code_locations = src tests
deps = .[dev]

[testenv:pytest]
description = Run unit tests
commands = pytest tests/

[testenv:ruff]
description = Ensure PEP-8 compliance
skip_install = true
deps = ruff
commands = ruff {[testenv]code_locations}

[testenv:mypy]
description = Ensure safety on types
commands = mypy {[testenv]code_locations}

[testenv:black]
description = Format code
skip_install = true
deps = black
commands = black {[testenv]code_locations}

[testenv:isort]
description = Format import order on code
skip_install = true
deps = isort
commands = isort {[testenv]code_locations}

[testenv:pyclean]
description = Clean up bytecode and build artifacts
skip_install = true
deps = pyclean
commands = pyclean .
```
