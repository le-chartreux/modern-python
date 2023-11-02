# Cleaning

As your mom tells you, chores aren't fun, but they have to be done.
Fortunately, they're going to go pretty fast in our case.

First of all, delete `create_welcome_message.py` and the references of its content.

The file `cleather/__init__.py` should be like the following:

```python
"""Public interface of cleather."""

__all__ = []
```

And `__main__.py` like the following:

```python
"""Executable of cleather."""


def main() -> None:
    """Welcome the user with its system name."""
    print("Hello, World!")
```

Now, running `cleather` should show `Hello, World!` in the console.

Congratulations, you've finished initializing your project!
To start the coding part of the project, refer to the [Chapter 2 - Code](../code/README.md).
