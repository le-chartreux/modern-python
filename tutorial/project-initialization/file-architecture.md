# File Architecture

- [File Architecture](#file-architecture)
  - [Language Agnostic](#language-agnostic)
  - [Language Specific](#language-specific)
    - [Private package](#private-package)
    - [Public package](#public-package)
      - [`__init__.py`](#__init__py)
      - [`__main__.py`](#__main__py)

## Language Agnostic

This section outlines the initial setup steps that are common to any project, regardless of the programming language you choose.

Start by creating a dedicated directory for your project.
In our case, we'll name it `cleather`.

```sh
mkdir cleather
cd cleather
```

While not mandatory, it's highly recommended to use a version control system for tracking changes in your project.
This tutorial exclusively focuses on Python development, and therefore, it does not provide guidance on using Git.
However, if you're interested in improving your Git workflow, you can explore resources like [Conventional Commits](https://www.conventionalcommits.org/) to enhance the cleanliness and structure of your version control practices.
We'll initialize [Git](https://git-scm.com/) to manage version control.

```sh
git init
```

Then you will need to create three files:

- `README.md`, to describe your project and provide the instructions on how to install and use it.
- `.gitignore`, tp specify which parts of your project's file system should be ignored by Git. You can use a predefined one, such as [this one](https://github.com/github/gitignore/blob/main/Python.gitignore) for Python.
- `LICENSE`, to protect your work with an open-source license. Visit [choosealicense](https://choosealicense.com/) to find the one that aligns with your project's goals. In this tutorial, we'll opt for the [MIT License](https://mit-license.org/).

Once you've completed these steps, your project's file structure should be the following:

```tree
cleather
├── .git
├── .gitignore
├── LICENSE
└── README.md
```

For now, let's provide a very minimalist description in our README.md:

```markdown
# cleather

Cleather is a Python terminal application designed to provide weather information for any location using the [OpenWeatherMap API](https://openweathermap.org/api).

**Please Note:** Cleather is currently under development and not yet functional.
We appreciate your interest and invite you to check back later for updates.

This project was created following the [Modern Python Tutorial](https://github.com/le-chartreux/modern-python/tree/with-tutorial/tutorial) by [le-chartreux](https://github.com/le-chartreux).
```

## Language Specific

Now, let's dive into the Python-specific configuration for our project.

Many popular Python projects, such as [pytest](https://github.com/pytest-dev/pytest) and [matplotlib](https://github.com/matplotlib/matplotlib), use the *src* layout.
However, other projects like [Django](https://github.com/django/django) and [numpy](https://github.com/numpy/numpy/tree/main) use the *flat* layout.
The choice between these layouts often comes down to personal preference.
For an in-depth comparison of the two, you can refer to the PyPA article [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

In our case, we will use the src layout because it allows for a cleaner organization of private packages.

In this architecture, sources are in a dedicated `src` folder (as expected from the *src* layout).

```sh
mkdir src
```

Within the `src` folder, you can have multiple packages, including the public package (`cleather`), the private package (`_cleather`), and any others as needed for your project (e.g. CLI, GUI, REST API, demonstration, etc.).
Since we are developing a simple CLI app, we will only create the public and the private package.

### Private package

The private package (_cleather) will house the core code of the project.

```sh
mkdir src/_cleather
```

As it's a package, create an `__init__.py` file to indicate that it's a package.

```sh
touch src/_cleather/__init__.py
```

Now, fill the `__init__.py` file with the following code:

```py
"""Private package of cleather."""
```

To test the configuration, create an additional file named `create_welcome_message.py`.
This file is temporary and is used to verify the configuration.

```sh
touch src/_cleather/create_welcome_message.py
```

Add the following code to create_welcome_message.py:

```py
def create_welcome_message(name: str) -> str:
    """Welcome the name by prepending 'Welcome to cleather' and appending '!'."""
    return f"Welcome to cleather {name}!"
```

With these steps, your project's code architecture should now resemble the following:

```tree
cleather
├── LICENSE
├── README.md
└── src
    └── _cleather
        ├── create_welcome_message.py
        └── __init__.py
```

### Public package

The public package (`cleather`) is an interface that contains almost no code.
It is used to offer users a clear and controlled API, and may also declare the main function if the package is executable with only one type of entry point (e.g. only CLI or only GUI).
Typically, the public package consists of one or two files: `__init__.py` and `__main__.py`.

To establish the `cleather` package, create a new directory within the `src` folder:

```sh
mkdir src/cleather
```

#### `__init__.py`

Just like any other Python package, the cleather package requires an `__init__.py` file:

```sh
touch src/cleather/__init__.py
```

The `__init__.py` file is responsible for importing specific elements from the `src/_cleather/` package that you want to expose to users.
This design allows users to interact with the API without needing to understand the internal project structure, and developers to freely modify the project's internal architecture without affecting the API.
Below is an example illustrating two ways to import from external code:

 ```py
# Using the internal structure
from _cleather.create_welcome_message import create_welcome_message
# -> Requires knowledge of the internal structure
# -> Affected by changes in the internal structure

# Using elements imported in the __init__.py 
from cleather import create_welcome_message
# -> Easier for users
# -> Not impacted by changes in the internal structure
```

To grant external access to the internal code from the `__init__.py` file, simply import the content you wish to expose.
To test our configuration, fill your `__init__.py` as follows, so the `create_welcome_message` will be exposed:

```py
"""Public interface of cleather."""

from _cleather.create_welcome_message import create_welcome_message
```

It's considered a good practice to add an `__all__` statement in your package to explicitly indicate which elements you intend to export.
Add the following line at the end of your `__init__.py`:

```py
__all__ = ["create_welcome_message"]
```

#### `__main__.py`

If the package is executable, the `__main__.py` defines a main function that parses arguments and utilizes some elements exposed by the `__init__.py`.
As cleather is executable, create a `__main__.py`:

```sh
touch src/cleather/__main__.py
```

Inside `__main__.py`, utilize the public interface to import the `create_welcome_message` function and utilize it in your application:

```py
"""Executable of cleather."""

from cleather import create_welcome_message


def main() -> None:
    """Welcome USER."""
    welcome_message = create_welcome_message("USER")
    print(welcome_message)
```

You might have observed that the typical `if __name__ == "__main__": main()` construct is not employed at the end of this file.
The reason for this is that in the next section, we will create a script that directly invokes the `main` function!

Congratulations!
You have now established a well-organized `src` file architecture.
At this point, your file structure should resemble the following:

```tree
.
├── LICENSE
├── README.md
└── src
    ├── _cleather
    │   ├── create_welcome_message.py
    │   └── __init__.py
    └── cleather
        ├── __init__.py
        └── __main__.py
```

You are now ready to proceed to the next section, which covers the [configuration of your project](configuration.md).
