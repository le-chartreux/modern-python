# File architecture

An intuitive file architecture is crucial for any project.
It enables developers to quickly find what they are looking for and saves time that would otherwise be wasted on figuring out where to create a new file.

Many popular Python projects, such as [pytest](https://github.com/pytest-dev/pytest) and [matplotlib](https://github.com/matplotlib/matplotlib), use the src layout
However, other projects like [Django](https://github.com/django/django) and [numpy](https://github.com/numpy/numpy/tree/main) use the flat layout.
Ultimately, the choice between the two layouts depends on personal preference.
You can find a PyPA article highlighting the key differences between the two layouts [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

This chapter focuses on using the src layout for a project.
While the flat layout is also a popular choice, the src layout allows for a cleaner declaration of private packages, which is why I prefer it.

The src layout for a package `my-package` looks like the following:

```txt
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

In this architecture, sources are in a dedicated `src` folder (as expected from the *src* layout).
The `src` folder contains multiple packages, including the [public package](#public-package) (`my_package`), the [private package](#private-package) (`_my_package`), and possibly others depending on the needs of the project (e.g. REST API, demonstration, etc.).
You can also notice that the structure of the `tests` folder mirrors the one in `src`, to easily find the test file of a module.

## Public package

The public package (`my_package`) is an interface that contains almost no code.
It is used to provide a clear and controlled API to the user, and may also declare the main function if the package is executable.
The public package contains usually one or two files: [`__init__.py`](#__init__py) and [`__main__.py`](#__main__py).

### `__init__.py`

The `__init__.py` imports the elements of `src/_my_package/` that you want to give access to the user.
This way the user does not have to know the internal architecture of the project, and the developers are free to modify the internal architecture as they want while the API does not change.

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

The private package (`_my_package`) contains the code of the project.
