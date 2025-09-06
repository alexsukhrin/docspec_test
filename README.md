docspec_test — pytest plugin for docstring code blocks

Run Python examples embedded in docstrings as tests. This plugin looks for fenced code blocks marked as:

```markdown
```python test
# your example here
```
```

It collects such blocks from functions and classes and executes them during pytest runs.

Why
----

Keep tests where they matter most: next to the API they validate. Docstring tests serve as living examples, documentation, and specification at once. When examples drift, tests fail, forcing alignment between docs and behavior.

Installation
------------

```bash
pip install docspec-test
```

Usage
-----

1) Add Python fenced blocks with the "test" info tag to your docstrings:

```python
def add(a: int, b: int) -> int:
    """
    Adds two numbers.

    ```python test
    assert add(1, 2) == 3
    ```
    """
    return a + b
```

2) Run pytest as usual; the plugin is auto-discovered via `pytest11` entry point:

```bash
pytest
```

Directives
----------

You can enrich test blocks with directives in the header:

```markdown
```python test name="custom-name" raises=ValueError skip="reason" xfail
# test code
```
```

- name: set a custom test name
- raises: assert an exception is raised (e.g. `raises=KeyError`)
- skip: mark test skipped (optionally with a reason)
- xfail: mark test expected to fail (optionally with a reason)

Setup/Teardown
--------------

Docstrings can also contain one optional setup and teardown block per object:

```markdown
```python setup
state = {"x": 0}
```

```python test name="increments"
state["x"] += 1
assert state["x"] == 1
```

```python teardown
state.clear()
```
```

Requirements
------------

- Python >= 3.8
- pytest >= 7.0.0

License
-------

MIT


