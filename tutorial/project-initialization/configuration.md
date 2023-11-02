# Configuration

The configuration of a Python project is crucial for ensuring that installation, development, and deployment are simple for contributors.
In 2016, [PEP 518](https://peps.python.org/pep-0518/) was introduced, specifying that the configuration of Python projects should be contained in a unified file named `pyproject.toml`.
This section will guide you throught setting up a project with a `pyproject.toml` file.

First of all, create a `pyproject.toml` file at the root of your project:

```sh
touch pyproject.toml
```

The `pyproject.toml` file can become quite extensive, but we'll start with a minimalist configuration.
As we progress through the tutorial and require additional features, we will revisit this file to add the necessary fields.

## Project

For now, most of what we need can be configured under the project section.
This section provides metadata about the project, which is utilized by various tools like PyPI.

Let's start by creating the project section:

```toml
[project]
```

Now, add some essential information about the project and its authors.
Be sure to update the authors' details to reflect your own identity:

```toml
name = "cleather"
description = "Terminal application designed to provide weather information for any location using the OpenWeatherMap API."
keywords = ["cli", "weather", "openweathermap", "api"]
requires-python = ">=3.10"
authors = [{name = "FIRSTNAME LASTNAME", email = "XXX@XXX.XXX"},]
```

Next, add a subsection for the project's homepage and its bug tracker.
These URLs will be displayed on the PyPI page of your project, so it's important to provide them.
If you are not using [GitHub](https://github.com/) (or a similar platform), you can omit this section.

```toml
[project.urls]
"Homepage" = "https://github.com/YOUR_USERNAME/YOUR_PROJECT"
"Bug Tracker" = "https://github.com/YOUR_USERNAME/YOUR_PROJECT/issues"
```

The most interesting part of the `pyproject.toml` at this stage is the `script` subsection.
As the name suggests, this is where you define the entry points for your application, which are the commands users will be able to execute from their terminal.
In our case, we want the `cleather` command to invoke the `main` function located in the `__main__` file of the `cleather` package.
To achieve this, add the following configuration to your `pyproject.toml`:

```toml
[project.scripts]
cleather = "cleather.__main__:main"
```

## Build-system

The `build-system` section is used to configure how your project will be packaged.
I commonly use [setuptool](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html) as it's widely adopted, but you can use a different build system and configure it within this section.

Add the following section to your `pyproject.toml`:

```toml
[build-system]
requires = ["setuptools>=45"]
build-backend = "setuptools.build_meta"
```

## Recap

At the end of this section, your `pyproject.toml` should resemble the following example.
Remember to replace my information with your own:

```toml
[project]
name = "cleather"
description = "Terminal application designed to provide weather information for any location using the OpenWeatherMap API."
keywords = ["cli", "weather", "openweathermap", "api"]
requires-python = ">=3.10"
authors = [{name = "Nathan Rousseau", email = "le-chartreux-vert@protonmail.com"},]

[project.urls]
"Homepage" = "https://github.com/le-chartreux/cleather"
"Bug Tracker" = "https://github.com/le-chartreux/cleather/issues"

[project.scripts]
cleather = "cleather.__main__:main"

[build-system]
requires = ["setuptools>=45"]
build-backend = "setuptools.build_meta"
```

Now that your project is correctly configured, you can proceed to install it.
Refer to the [installation](installation.md) section for guidance on how to do that!
