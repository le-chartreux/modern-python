# Structure

To ensure ease of maintenance and contribution,  it's important that your tests follow a structure on their [name](#name), [content](#content) and [documentation](#documentation). You can refer to the [example of a unit test](#example-of-unit-test) at the end of this chapter for a practical demonstration.

## Name

On major unit test frameworks, test functions must begin with `test_`. The format I use is `test_functionname_executioncase`. This naming convention makes it easy to identify the function being tested and the specific execution case, especially when reading the logs.

## Content

Tests must be atomic: you should write one test function per execution case of the element you are testing. This approach makes it easier to identify and isolate any issues that may arise during testing.

## Documentation

Tests should be documented: write at least a short docstring starting with "It" to explain the expected behavior.

## Example

```python
def test_from_preferences_os_unsupported(monkeypatch: pytest.MonkeyPatch) -> None:
    """It can't search preferred language on an unsupported os."""
    monkeypatch.setattr(os, "name", "unsupported")
    with pytest.raises(RuntimeError):
        Language.from_preferences()
```

Source: [test_language.py by le-chartreux on hypermodern-python-tuto](https://github.com/le-chartreux/hypermodern-python-tuto/blob/master/test/wikipedia/test_language.py).