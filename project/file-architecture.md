# File architecture

Using an intuitive file architecture is a crucial aspect of any project. It enables developers to quickly find what they are looking for and saves time that would otherwise be wasted on figuring out where to create a new file.

This chapter focuses on using the src layout for a project. While the flat layout is also a popular choice, I prefer the src layout because it allows a cleaner declaration of private modules. You can find a PyPA article highlighting the key differences between the two layouts [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

## Shape

The src layout for a package 'my-package' looks like that:

```sh
.
├── docs/
│    └── ...
├── src/
│    ├── my-package/
│    │  ├── __init__.py
│    │  └── __main__.py
│    └── _my-package/
│       ├── __init__.py
│       └── ...
├── tests/
│    ├── my-package/
│    │  └── ...
│    └── _my-package/
│       └── ...
├── README.md
├── pyproject.toml
└── ...  # other config files
```
