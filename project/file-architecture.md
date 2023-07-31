# File architecture

Using an intuitive file architecture is an important quality for your project: it allows developers to quickly find what they search, and to don't waste time thinking of where to create a new file.
This chapter is about using the src layout on a project. The other popular choice is the flat layout, but I do prefer the src layout because it allows to declare private modules on a much cleaner way. You can find a PyPA article about the key diferences [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

## Shape

The src layout for a package 'my-package' looks like this:

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
