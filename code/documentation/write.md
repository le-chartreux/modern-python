# Write

A good documentation must be [formatted](#format) and [concise](#short). Do not hesitate to illustrate it with [examples](#examples). You can find [there](#example-with-google-style) a complete example of a good documentation.

## Format

Each public element have a [docstring](https://peps.python.org/pep-0257/), following one of the many available formats such as [Google](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings), [Epytext](https://epydoc.sourceforge.net/manual-epytext.html), [reStructuredText](https://peps.python.org/pep-0287/) or [Numpy](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard). Choose one of them that suits your style and stick to it consistently. 

## Short

Do not over comment the code: explain technical choices (name of the algorithm, design pattern used, etc.) and consequences of them (e.g. `:warning: very precise but slow, if a margin error of up to 2% is not a problem consider using XXX instead`). If you think that the content of a function needs to be commented for other reasons, consider simplifying it and using more relevant names before writing the comment.

## Examples

Write examples with [doctests](https://docs.python.org/3/library/doctest.html) and execute them with [pytest](../test/tools.md). Running them allows checking that the examples are still working.

## Example with Google style

```py
@classmethod
def from_preferences(cls) -> Self:
    """Search for the preferred language in the computer's settings.

    Since the computer settings vary a lot depending on the operating system,
    this function works on posix and Windows only.

    Returns:
        The preferred language.

    Raises:
        RuntimeError: If the os name is not posix nor Windows.

    Examples:
        >>> language = Language.from_preferences()
        >>> isinstance(language, Language)
        True
    """
    if os.name == "posix":
        return cls._from_preferences_posix()
    if os.name == "nt":
        return cls._from_preferences_windows()
    error_message = f"Unsupported operating system: {os.name}."
    raise RuntimeError(error_message)
```

Source: [language.py by le-chartreux on hypermodern-python-tuto](https://github.com/le-chartreux/hypermodern-python-tuto/blob/master/src/hypermodern_python_tuto/wikipedia/language.py#L16).
