# Write

Effective documentation should be well-[formatted](#format) and [concise](#conciseness), with [examples](#examples) to illustrate your points. You can find at the end of this chapter a [complete example of an effective documentation using Google style guidelines](#example-with-google-style).

## Format

Each public element should have a [docstring](https://peps.python.org/pep-0257/), following one of the many available formats such as [Google](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings), [Epytext](https://epydoc.sourceforge.net/manual-epytext.html), [reStructuredText](https://peps.python.org/pep-0287/), or [Numpy](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard). Choose one that suits your style and stick to it consistently.

## Conciseness

When commenting your code, avoid excessive details and focus on explaining technical choices such as the algorithm or design pattern used, along with any relevant consequences (e.g. `:warning: very precise but slow, if a margin error of up to 2% is not a problem consider using XXX instead`). If you feel that a function requires additional comments, consider simplifying the code and using more descriptive names before resorting to comments.

## Examples

When providing examples, use [doctests](https://docs.python.org/3/library/doctest.html) and execute them with [pytest](../test/execution.md) to ensure they are still functional. This is an effective way to check that your documentation stays up-to-date.

## Example with Google style

```py
@classmethod
def from_preferences(cls) -> Self:
    """Search for the preferred language in the computer's settings.

    Since the computer settings vary a lot depending on the operating system,
    this function works on POSIX and Windows only.

    Returns:
        The preferred language.

    Raises:
        RuntimeError: If the os name is not POSIX nor Windows.

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
