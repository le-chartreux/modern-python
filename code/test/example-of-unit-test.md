# Example of unit test

```python
def test_from_preferences_os_unsupported(monkeypatch: pytest.MonkeyPatch) -> None:
    """It can't search preferred language on an unsupported os."""
    monkeypatch.setattr(os, "name", "unsupported")
    with pytest.raises(RuntimeError):
        Language.from_preferences()
```

Source: [test_language.py by le-chartreux on hypermodern-python-tuto](https://github.com/le-chartreux/hypermodern-python-tuto/blob/master/test/wikipedia/test_language.py).
