# Coding Styles for Python
The following are coding guidelines that MUST be followed for all instances (files and coding examples) of the programming language Python.

- If you were to create a vanilla class, use `@dataclass` from `dataclasses` for defining the class.
- For `@dataclass` always use the `slots=True` parameter always. If applicable for the given class, then also use: `frozen=True`.
- Any code that has type annotations should use the modern variations (3.10+), as an example, avoid using `Union[A, B]` and use `A | B` instead.
- When constructing test cases, always use 'test-table'-signature (commonly used in Go). Please see the topic 'Test-table Example' for concrete details on this.

## Test-table Example
When constructing any type of test case, use a similar structure like seen below with the use of a class and pytest.parameterize.
```python
def add(a: int, b: int) -> int:
    return a + b

@dataclass(slots=True, frozen=True, kw_only=True)
class AddTestCase:
    name: str # <-- should exists for every kind of test
	input: tuple[int, int]
	expected_output: int



@pytest.mark.parameterize([
    AddTestCase(
	   name="2 + 2 = 4",
	   input=(2, 2),
	   expected_output=4,
	)
], ids=lambda tc: tc.name)
def test_add(tc: AddTestCase):
    output = add(*tc.input)
	assert output == tc.expected_output
```
