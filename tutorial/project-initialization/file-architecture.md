# File Architecture

- [File Architecture](#file-architecture)
  - [Language Agnostic](#language-agnostic)
  - [Language Specific](#language-specific)
    - [Private package](#private-package)
    - [Public package](#public-package)
      - [`__init__.py`](#__init__py)
      - [`__main__.py`](#__main__py)

## Language Agnostic

This part highlight setup that you will do on any project with any language.

First of all, create the directory for your project - our will be `cleather`.

```sh
mkdir cleather
cd cleather
```

Then initialize [Git](https://git-scm.com/) to get some version control.
This is not required, but I strongly recommand to use a version control system.

```sh
git init
```

Then you will need to create three files:

- `README.md`, a description of your project and the ways to install it to your users.
- `.gitignore`, the list of filesystem elements that Git will ignore. You can use [this one](https://github.com/github/gitignore/blob/main/Python.gitignore).
- `LICENSE`, to protect your work. Refer to [choosealicense](https://choosealicense.com/) to find the one that suits you. I will go for the [MIT License](https://mit-license.org/).

Now your file structure should be the following:

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

Terminal application that allows to get the weather of any place, using the [OpenWeatherMap API](https://openweathermap.org/api).

Currently in development and unusable.
Come back later!
```

## Language Specific

Now, let's dig onto the Python-specific configuration.

First of all, we will setup the file architecture of our project.

An intuitive file architecture is crucial for any project.
It enables developers to quickly find what they are looking for and saves time that would otherwise be wasted on figuring out where to create a new file.

Many popular Python projects, such as [pytest](https://github.com/pytest-dev/pytest) and [matplotlib](https://github.com/matplotlib/matplotlib), use the src layout.
However, other projects like [Django](https://github.com/django/django) and [numpy](https://github.com/numpy/numpy/tree/main) use the flat layout.
Ultimately, the choice between the two layouts depends on personal preference.
You can find a PyPA article highlighting the key differences between the two layouts [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

We will use the `src` layout because it allows for a cleaner declaration of private packages.

In this architecture, sources are in a dedicated `src` folder (as expected from the *src* layout).

```sh
mkdir src
```

The `src` folder contains multiple packages, including the [public package](#public-package) (`cleather`), the [private package](#private-package) (`_cleather`), and possibly others depending on the needs of the project (e.g. REST API, demonstration, etc.).
Because we are making a simple CLI app, we will only create the public and the private package.

### Private package

The private package (`_cleather`) will contain the code of the project.

```sh
mkdir src/_cleather
```

Because it is a package, create an `__init__.py` file.

```sh
touch src/_cleather/__init__.py
```

Then fill the `__init__.py` file with the following code.

```py
"""Private package of cleather."""
```

To test the configuration, create an additional file `create_welcome_message.py`.
This file will not last long, it is only used to test the configuration.

```sh
touch src/_cleather/create_welcome_message.py
```

Then fill it with the following code:

```py
def create_welcome_message(name: str) -> str:
    """Given a name, welcome it by prepending 'welcome to cleather' postponing '!'."""
    return f"welcome to cleather {name}!"
```

At this point, you should have the following code architecture:

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
It is used to provide a clear and controlled API to the user, and may also declare the main function if the package is executable.
The public package contains usually one or two files: [`__init__.py`](#__init__py) and [`__main__.py`](#__main__py).

```sh
mkdir src/cleather
```

#### `__init__.py`

Like every Python package, your public package needs an `__init__.py`.

```sh
touch src/cleather/__init__.py
```

The `__init__.py` imports the elements of `src/_cleather/` that you want to give access to the user.
This way the user does not have to know the internal architecture of the project, and the developers are free to modify the internal architecture as they want while the API does not change.
You can find bellow an example of the two ways to import from an external code.

 ```py
# using the internal structure
from _cleather.create_welcome_message import create_welcome_message
# -> need to know the internal strucutre of the package
# -> impacted by changes on the internal structure

# using the elements imported in the __init__.py 
from cleather import create_welcome_message
# -> easy
# -> not impacted by changes on the internal structure
```

To give external access to the internal code from the `__init__.py` file, simply import the content you want.
Because to test our configuration we want to be able to use the `create_welcome_message` function, fill your `__init__.py` like the following:

```py
"""Public interface of cleather."""

from _cleather.create_welcome_message import create_welcome_message
```

It is considered a good practice to add an `__all__` statement on your package to explicitly indicate which elements you want to export, so add the following line at the end of your `__init__.py`:

```py
__all__ = ["create_welcome_message"]
```

#### `__main__.py`

If the package is executable, the `__main__.py` defines a main function that parses args and uses some elements imported by the `__init__.py`.
Because `cleather` is executable, create a `__main__.py`:

```sh
touch src/cleather/__main__.py
```

Inside `__main__.py`, use the **public** interface to import the `create_welcome_message` function and use it.

```py
"""Executable of cleather."""

from cleather import create_welcome_message


def main() -> None:
    """Welcome USER."""
    welcome_message = create_welcome_message("USER")
    print(welcome_message)


if __name__ == "__main__":
    main()
```

Congrats, you now have a `src` file architecture!
At this point, your file architecture should be the following:

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
