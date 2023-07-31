# File architecture

Using an intuitive file architecture is a crucial aspect of any project.
It enables developers to quickly find what they are looking for and saves time that would otherwise be wasted on figuring out where to create a new file.

Many popular Python projects, such as [pytest](https://github.com/pytest-dev/pytest) and [matplotlib](https://github.com/matplotlib/matplotlib), use the src layout
However, other projects like [Django](https://github.com/django/django) and [numpy](https://github.com/numpy/numpy/tree/main) use the flat layout.
Ultimately, the choice between the two layouts depends on personal preference.
You can find a PyPA article highlighting the key differences between the two layouts [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

This chapter focuses on using the src layout for a project.
While the flat layout is also a popular choice, I prefer the src layout because it allows a cleaner declaration of private packages.

The src layout for a package `my-package` looks like the following:

```sh
my-package/
 │
 ├── docs/
 │    └── ...
 │
 ├── src/
 │    ├── my_package/
 │    │  ├── __init__.py
 │    │  └── __main__.py
 │    │
 │    └── _my_package/
 │       ├── __init__.py
 │       ├── file_a.py
 |       └── subfolder/
 │           └── file_b.py
 │
 ├── tests/
 │    ├── my_package/
 │    │  ├── test___init__.py
 │    │  └── test___main__.py
 │    │
 │    └── _my_package/
 │       ├── test___init__.py
 │       ├── test_file_a.py
 |       └── subfolder/
 │           └── test_file_b.py
 │
 ├── README.md
 ├── pyproject.toml
 └── ...  # other config files
```

With this architecture, sources are in a dedicated `src` folder (as we can expect from the *src* layout).
The `src` folder contains multiple packages: the [public package](#public-package) (`my_package`), the [private package](#private-package) (`_my_package`), and maybe others packages depending on needs (e.g. REST API, demonstration, etc.).
You can also notice that the structure of the `tests` folder mirrors the one in `src`, to easily find the test file of a module.

## Public package

The public package (`my_package`) is an interface that almost don't contain code.
It is used to provide a clear and controled API to the user: this way the user does not have to know the internal architecture of the project, and the developers are free to modify the internal architecture as they want while the API does not changes.
The public package contains usually one or two files: [`__init__.py`](#__init__py) and [`__main__.py`](#__main__py).

### `__init__.py`

 The `__init__.py` imports the elements of `src/_my_package/` that you want to give access to the user.
 This way the user will be able easily import element without caring about the internal structure of the package:

 ```py
# using the internal structure
from my_package.subfolder.file_b import element_from_b
# -> need to know the internal strucutre of the package
# -> impacted by changes on the internal structure

# using the elements imported in the __init__.py 
from my_package import element_from_b
# -> easy
# -> not impacted by changes on the internal structure
```

### `__main__.py`

If the package is executable, the `__main__.py` defines a main function that parses args and uses some elements imported by the `__init__.py`.

## Private package

The private package (`_my_package`) contains the true code of the project.
