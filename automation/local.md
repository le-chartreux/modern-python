# Local

When it comes to running a sequence of actions, there are several options available, ranging from basic shell files to more sophisticated tools like [Make](https://www.gnu.org/software/make/manual/make.html).
However, for local Python project execution, my personal favorite is [Tox](https://tox.wiki/).

While there are other Python-specific tools like [Nox](https://nox.thea.codes/en/stable/) available, I find that they lack maturity and can be overly verbose compared to [Tox](https://tox.wiki/).
In my opinion, the benefits of using a non-standard tool like [Nox](https://nox.thea.codes/en/stable/) are not significant enough to justify the migration effort and the potential risk of end-of-support.
[Nox](https://nox.thea.codes/en/stable/) is essentially a copy of [Tox](https://tox.wiki/) with a Python script for configuration instead of an `ini` file, but some of its functions may not work as intended.

## Tox

You can see [Tox](https://tox.wiki/) as a [make](https://www.gnu.org/software/make/manual/make.html) specialized for Python, that allows you to use virtual environments and run actions across multiple Python versions.

### Usage

[Tox](https://tox.wiki/) is a user-friendly tool that is easy to use.
While you can find more commands in the [Tox user guide](https://tox.wiki/en/latest/user_guide.html) or the [documentation of the Tox CLI](https://tox.wiki/en/latest/cli_interface.html), there are three main commands to remember:

```sh
# run all the actions of env_list
tox
# run all the actions of the <format> label
tox -m format
# run the <pytest> action
tox -e pytest
```

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
