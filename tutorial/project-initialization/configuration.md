# Configuration

The configuration of a Python project is crucial for ensuring that installation, development, and deployment are simple for contributors.
In 2016, [PEP 518](https://peps.python.org/pep-0518/) was introduced, which specified that the configuration of Python projects should be contained in a unified file named `pyproject.toml`.
This section explains how to set up a project with a `pyproject.toml` file.

First of all, create a `pyproject.toml` file at the root of your project:

```sh
touch pyproject.toml
```

A `pyproject.toml` can be huge, but we will start gentle with a minimalist configuration.
When we will need new features in the following of the tutorial, we will go back to this file and create the required fields.

## Project

For now, almost everything we need will be on the `project` section.
It provides metadata about the project, that is used by different tools like PyPI.

Let's start by creating the `project` section:

```toml
[project]
```

Then, under the section, add some information about the project and its authors.
Don't forget to modify the authors so it matches your identity:

```toml
name = "cleather"
description = "Terminal application designed to provide weather information for any location using the OpenWeatherMap API."
keywords = ["cli", "weather", "openweathermap", "api"]
requires-python = ">=3.10"
authors = [{name = "FIRSTNAME LASTNAME", email = "XXX@XXX.XXX"},]
```

Now, let's add a subsection for the homepage of your project and its bug tracker.
These URLs will be put on the PyPI page of your project, so it's important to specify them.
If you don't use [GitHub](https://github.com/) (or any other similar tool), don't put this section.

```toml
[project.urls]
"Homepage" = "https://github.com/YOUR_USERNAME/YOUR_PROJECT"
"Bug Tracker" = "https://github.com/YOUR_USERNAME/YOUR_PROJECT/issues"
```

For now, the most interesting part of the `pyproject.toml` is the `script` section.
As its name suggest, it's where you will define the entry points of your application, and so the commands the user will be able to run.
To allow your user to run the `cleather` command, add the following to your `pyproject.toml`.

```toml
[project.scripts]
cleather = "cleather.__main__:main"
```

## Build-system

The `[build-system]` section is where you can configure your build system (obviously).
I use [setuptool](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html) as it's the most commonly used, but you can use another build system and configure it in this section.

Add the following section to your `pyproject.toml`:

```toml
[build-system]
requires = ["setuptools>=45"]
build-backend = "setuptools.build_meta"
```

## Recap

At the end of this section, your `pyproject.toml` should look like the following, except that you filled your personnal information instead of mines:

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

Because your project is correctly configured, you can now [install](installation.md) it!
Refer to the [installation](installation.md) section to learn how to!
