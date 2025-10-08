---
applyTo: '**/.py
---

# Format
- Obey `ruff` with length up to 120
- If fucntion signature/calling can not fit in one line, put each argument in a separate line

## Naming
- Prepend private class methods with `_`

## Import
- All import should be on top of the file
- For non-testing code, use relative import for module under the same directory, otherwise use absolute import.
- Do not use wildcard import
- For `__init_.py` , do not use `__all__`  but append `#ruff: noqa: F401` to import to suppress unused import warning

## Function order
Follow these rules to order functions/methods in a file/class, the earlier the higher priority:
1. public methods should be placed before private methods
2. caller methods should be placed before callee methods

# Readability

## Docstrings
- Use Google style docstrings
- Assure every function or method has its docstring
- Assure every doctrsing complies with current signature and implementation

## Type Hinting
- Assure type hinting for all function arguments and return values
- Assure type hinting for declaration of variable of nested container type
- Use `|` instead of `Union` for union type hinting
- Use `Optional` only when the default value is `None`, otherwise use union type hinting when `None` is one of the possible types
- When a variable can only take a fixed set of values, type hint it with `Literal` when value set won’t be reused across many places or extended later, otherwise use `Enum`

## Comment on complex variable
- Comment nestedly structured variable to give meaning to each level. E.g., `employees: List[Dict[str, List[str]]] = ... # (number of companys, departement: (number of employees))`
- Comment multi-dimensional variable, such as `ndarray` or `Tensor`, to specify data type (if it not float-like) and give meaning to each dimension, e.g., `input_ids = ... # <int>(batch_size, seq_len)`, `hidden_states = ... # (batch_size, seq_len, hidden_size)`
- Comment these complex variables immediately after their declarations or assignments in signatures, body, or return statements to give meaning to each level or dimension. E.g., 
    ```
    def forward(
        self, 
        input_ids: Tensor # <int>(batch_size, seq_len),
        attention_mask: Optional[Tensor] = None # <bool>(batch_size, seq_len)
    ) -> Tensor # (batch_size, seq_len, hidden_size)
    ```

# Principles
- Follow DRY (Don't Repeat Yourself) principle. If you should change the other part of code when you change one part of code, they should be refactored into one reusable component. You can identify it by comparing their inputs, outputs, intents, usage scenarios, or logics.
- Follow YAGNI (You Aren't Gonna Need It) principle. Do not add functionality and logics that are not explicitly required or necessary for the program to work.
- Follow KISS (Keep It Simple, Stupid) principle. Prefer readability and **compactness** over future extensibility.
- Follow SOLID principles on designing objects.