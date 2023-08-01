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

Dynamic attributes are computed during the building of a project.
The dynamic field indicates that the given element names are added by some tools at the time of building the project.

For instance, in the example above, the version is computed to avoid writing it in multiple places and potentially forgetting to update it when bumping the version.
But where should we store this version number, if not in the `pyproject.toml`?
The tool that suit this job the best is obviously our version manager.
To use dynamic version based on VCS, follow these steps:

1) Add  `"version"` to the `dynamic` attribute.
2) Append a section `[tool.setuptools_scm]` later in the `pyproject.toml`.
3) Specify in the `build-system.requires` section that `setuptools_scm[toml]>=6.2` is required.

### Dependencies

The `dependencies` attribute specifies mandatory dependencies required to use the project.
You can specify particular version numbers (equal, superior, inferior).
If you don't specify a version number and the user does not have the dependency installed, the latest version will be downloaded automatically.

### Optional dependencies

In the  `[project.optional-dependencies]` section, you can define multiple optional dependency groups.
These optional dependency groups will not be downloaded by default.
The most common is `dev` dev group, but you can create others as well (e.g. for an app that uses audio, the mp3 format can be in the standard distribution but the libraries for the flak format can be optional).
Similarly to the [dependencies](#dependencies) attribute, you can specify particular version numbers.

### Scripts

In the `[project.scripts] section, you can define entry points of executables for your project.
When the project is installed, the user will be able to execute the scripts by running the name of the command (here`my-project`).

## Tool

The `[tool]` section contains configurations for the tools you will use on your project, such as [formatter](../code/format.md), [type-checker](../code/type-check.md), [test runner](../code/test/execution.md), etc.
Here, we only have `[tool.setuptools_scm]`, which is empty because we want to keep the default configuration.
However, when following the [code](../code/README.md) part of this tutorial, you will fill it.

## Build-system

The `[build-system]` section is where you can configure your build system (obviously).
I use [setuptool](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html) as it's the most commonly used, but but you can use another build system and configure it in this section.
