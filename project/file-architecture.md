# File architecture

Using an intuitive file architecture is a crucial aspect of any project. It enables developers to quickly find what they are looking for and saves time that would otherwise be wasted on figuring out where to create a new file.

Many popular Python projects, such as [pytest](https://github.com/pytest-dev/pytest) and [matplotlib](https://github.com/matplotlib/matplotlib), use the src layout. However, other projects like [Django](https://github.com/django/django) and [numpy](https://github.com/numpy/numpy/tree/main) use the flat layout. Ultimately, the choice between the two layouts depends on personal preference. You can find a PyPA article highlighting the key differences between the two layouts [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

This chapter focuses on using the src layout for a project. While the flat layout is also a popular choice, I prefer the src layout because it allows a cleaner declaration of private packages.

## Shape

The src layout for a package `my-package` looks like the following:

```sh
.
├── docs/
│    └── ...
├── src/
│    ├── my_package/
│    │  ├── __init__.py
│    │  └── __main__.py
│    └── _my_package/
│       ├── __init__.py
│       └── 
├── tests/
│    ├── my_package/
│    │  └── ...
│    └── _my_package/
│       └── ...
├── README.md
├── pyproject.toml
└── ...  # other config files
```
