# PEP 8 compliance

[PEP 8](https://pep8.org/) is a set of rules for writing Pythonic code.
To ensure that the code adheres to these rules, you can use a static analysis tool called a [linter](https://en.wikipedia.org/wiki/Lint_(software)).
While the two most commonly used Python linters are [pylint](https://pypi.org/project/pylint/) and [flake-8](https://flake8.pycqa.org/en/latest/), I prefer to use a different one: [Ruff](https://beta.ruff.rs/docs/).

## Ruff

[Ruff](https://beta.ruff.rs/docs/) has several advantages:

- Support for [pylint](https://pypi.org/project/pylint/) and [flake-8](https://flake8.pycqa.org/en/latest/) rules.
- Faster checking, 10 to 100 times faster than [pylint](https://pypi.org/project/pylint/) and [flake-8](https://flake8.pycqa.org/en/latest/).
- No need for additional plugins, because they are already shipped with [Ruff](https://beta.ruff.rs/docs/).

### Usage

```sh
ruff .
```

### Configuration

Add the following configuration to your `pyproject.toml`, with `"YOUR PACKAGE NAME"` in `tool.ruff.isort` replaced with your package name (of course), and the same for `"MAYBE PRIVATE NAME OF YOUR PACKAGE"` if you have some private packages.

```toml
[tool.ruff]
select = [
    "A", # flake8-builtins (redefinition of bultins)
    "ANN", # flake8-annotations (type annotations are everywhere)
    "ARG", # flake8-unused-arguments (unused argument in function/method/class/lambda)
    "B", # flake8-bugbear (bugs & design problems)
    "B9", # flake8-bugbear strict (bugs & design problems)
    "BLE", # flake8-blind-except (no "except:" or "except Exception:")
    # "COM", # flake8-commas (force trailing commas) -> unelegant
    "C4", # flake8-comprehensions (better list/set/dict comprehensions)
    "C90", # McCabe (code complexity)
    "D", # pydocstyle (documentation style)
    "DJ", # flake8-django (practices on Django)
    "DTZ", # flake8-datetimez (usage of unsafe naive datetime class)
    "E", # pycodestyle (violation of PEP-8)
    "EM", # flake8-errmsg (format error messages)
    "EXE", # flake8-executable (executable permissions and shebangs)
    "ERA", # eradicate (no commented-out code)
    "F", # pyflakes (invalid Python code)
    "FBT", # flake8-boolean-trap (misusage of booleans in function declaration & calls)
    "G", # flake8-logging-format (logging format strings)
    "I", # isort (import order)
    "ICN", # flake8-import-conventions (how certain packages should be imported or aliased)
    # "INP", # flake8-no-pep420 (ban PEP-420 implicit namespace packages) -> long live implicit namespace packages!
    "INT", # flake8-gettext (f-string resolved before function calls)
    "ISC", # flake8-implicit-str-concat (string literal concatenation)
    "N", # pep8-naming (naming conventions)
    "NPY", # NumPy-specific rules (e.g. deprecated-type-alias and legacy-random)
    "PD", # pandas-vet (pandas code)
    "PIE", # flake8-pie (miscellaneous lints)
    "PGH", # pygrep-hooks (miscellaneous lints, e.g. "use specific rule codes when using noqa")
    "PL", # Pylint (static code analyser)
    "PT", # flake8-pytest-style (style issues or inconsistencies with pytest-based tests)
    "PTH", # flake8-use-pathlib (use of functions that can be replaced by pathlib module)
    "PYI", # flake8-pyi (provide specializations for type hinting stub files)
    "Q0", # flake8-quotes (avoid escaping quotes)
    "RSE", # flake8-raise (improvements for raise statements)
    "RET", # flake8-return (check return values)
    "RUF", # ruff-specific rules
    "S", # flake8-bandit (security)
    "SIM", # flake8-simplify (tips to simplify the code)
    "SLF", # flake8-self (private member access)
    "T10", # flake8-debugger
    "T20", # flake8-print (no print nor pprint)
    "TCH", # flake8-type-checking (move import only intended for type-checking in "if TYPE_CHECKING" blocs)
    "TID", # flake8-tidy-imports (ordonated imports)
    "TRY", # tryceratops (exception handling AntiPatterns)
    "UP", # pyupgrade (upgrate syntax for newer versions of Python)
    "YTT", # flake8-2020 (misuse of sys.version and sys.version_info)
    "W" # pycodestyle (violation of PEP-8)
]
ignore = [
    "ANN101", # missing type annotation for self, but hinting self all the time is useless
    "ANN102", # missing type annotation for cls but hinting cls all the time is useless
    "ANN401", # disallows Any, but some elements should be Any when they are external
    "B024",   # forces abstract classes to have at least one abstract method, but sometimes a class is virtually abstract
    "D100",   # docstrings at the top of public modules, but most of the time it's useless
    "D105",   # docstrings on magic methods, useless docstrings are well known 
    "E501",   # line size, but bug-bear already set it with a tolerance of 10% (B950)
    "PD011 ", # use .to_numpy instead of .values, but raises a lot of false positives
]

[tool.ruff.per-file-ignores]
"docs/conf.py" = [
    "A001" # redefine some builtins (like "copyright") is OK in docs
]
"test*/" = [
    "ARG", # some arguments are unused in tests functions but useful (e.g. mocks)
    "S101", # asserts are OK for tests
    "SLF001" # accessing private members is OK for tests
]

[tool.ruff.pydocstyle]
convention = "google"

[tool.ruff.isort]
known-first-party = ["YOUR PACKAGE NAME", "MAYBE PRIVATE NAME OF YOUR PACKAGE"]
```
