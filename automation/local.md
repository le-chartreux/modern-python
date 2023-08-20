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
While you can find more commands in the [Tox user guide](https://tox.wiki/en/latest/user_guide.html) or the [documentation of the Tox CLI](https://tox.wiki/en/latest/cli_interface.html), there are main commands to remember:

```sh
# run all the actions of env_list
tox
# run all the actions of the <format> label
tox -m format
# run the <pytest> action
tox -e pytest
# list the available actions
tox list
```

### Configuration

Configuring [Tox](https://tox.wiki/) for your project is easy.
Simply create a `tox.ini` file at the root of your project and fill it with the following sections:

- [`[tox]`](#tox-1), the general options for [Tox](https://tox.wiki/).
- [`[testenv]`](#testenv), the default configuration for your actions.
- [`[textenv:action]`](#testenvaction), the specific actions that will be run.

For more detailed information on configuring Tox, refer to the [Tox user guide](https://tox.wiki/en/latest/user_guide.html).

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

#### `[tox]`

The `[tox]` section defines general options for [Tox](https://tox.wiki/), mainly configurations regarding the `tox` command:

- `env_list` defines which actions to run by default (when no particular action is specified).
- `labels` specify which action is linked to which label.

#### `[testenv]`

The `[testenv]` section defines the default configuration for your actions.
Defining a field in `[testenv:action]` that is already defined in `[testenv]` will overwrite it.
In our case, we specify two fields:

- `code_locations`, to indicate where our code is stored.
- `deps`, to specify the dependencies required to run our actions.

#### `[testenv:action]`

The `[testenv:action]` section is where you define the specific actions that will be run by [Tox](https://tox.wiki/).
Each action has the following options:

- `description`: a brief description of the action that will be displayed when using the `tox list` command.
- `commands`: the command or commands to run for the action. Commands can be multiline and can include [Tox](https://tox.wiki/) parameters using curly brackets.
- `skip_install`: a boolean option that indicates whether installing the project is necessary to run the action. For example, the `pyclean` action does not require installation, since it only cleans up temporary Python files.
- `deps`: if the dependencies required for the action are different from those defined in `[testenv]`, you can specify them here.

Defining actions in `[testenv:action]` is the main goal of [Tox](https://tox.wiki/), allowing you to easily define and run specific tasks for your project.
