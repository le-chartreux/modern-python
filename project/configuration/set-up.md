# Set up

To set up a project with a `pyproject.toml` file, you will need to create a file with the following structure:

```toml
[project]
name = "my-project"
description = "Blablabla."
authors = [{name = "FIRSTNAME LASTNAME", email = "XXX@XXX.XXX"},]
keywords = ["keyword1", "keyword2"]
requires-python = ">=3.10"
dynamic = ["version"]

dependencies = ["dependency1>=13.2", "dependency2=1.0.0", "dependency3",]

[project.optional-dependencies]
dev = ["dev-dependency1", "dev-dependency2>=2.1",]

[project.scripts]
my-project = "my-project.__main__:main"

[tool.setuptools_scm]
# this section should exist even if it is empty to allow setuptools_scm to work

[build-system]
requires = ["setuptools>=45", "setuptools_scm[toml]>=6.2"]
build-backend = "setuptools.build_meta"
```

The `pyproject.toml` file is divided in three main parts: [`[project]`](#project), [`[tool]`](#tool), and [`[build-system]`](#build-system).

## Project

The `[project]` section provides metadata about the project, that is used by different tools like PyPI.
The two particular attributes that are detailed are [dynamic](#dynamic) and [dependencies](#dependencies), along with the parts [`[project.optional-dependencies]`](#optional-dependencies) and [`[project.script]`](#scripts).
For more information on each attribute and part, refer to the [PyPA specification](https://packaging.python.org/en/latest/specifications/declaring-project-metadata/).

### Dynamic

Dynamic attributes are computed ones.
In our case, we compute the version to don't write it at multiple places (and so divide our risks to forget to bump one when releasing).
But where should we store this version number if not in the `pyproject.toml`?
The tool that suit this job the best is obviously our version manager.
All we have to is to add `"version"` to the `dynamic` attribute, add `[tool.setuptools_scm]` later in our `pyproject.toml`, and specify in the `build-system.requires` part that we need `setuptools_scm[toml]>=6.2`.

### Dependencies

The `dependencies` attribute specifies dependencies that are mandatory to use the project.
You can specify particular version numbers (equal, superior, inferior).
If you don't and the user does not have the dependency installed, the latest version will be downloaded.

### Optional dependencies

In the `[project.optional-dependencies]` part, you can define multiple optional dependency groups.
These optional dependency groups will not be downloaded by default.
The most common is the `dev` group, but you can think of others (e.g. for an app that uses audio, the mp3 format can be in the standard distribution but the libraries for the flak format can be optional).
Similarly to the [dependencies](#dependencies) attribute, you can specify particular version numbers.

### Scripts

In the `[project.scripts]` part, you can define entry points of executables of your project.
When the project will be installed, the user will be able to execute the scripts by running the name of the command (here `my-project`).

## Tool

The [tool] part contains the configurations for the tools you will use on your project: [formatter](../code/format.md), [type-checker](../code/type-check.md), [test runner](../code/test/execution.md), etc.
Here we only have `[tool.setuptools_scm]`, that is empty because we want to keep the default configuration, but when following the [code](../code/README.md) part of this tutorial you will fill it.

## Build-system

The `[build-system]` is where you can configure your build system (obviously).
I use [setuptool](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html) to build my system because it's the most used, but if you want to use another one this section is where you will configure it.
