---
mode: agent
description: Generate or modify testing code and production code based on the given specifications.
---
Your goal is to make sure specifications, testing code, and production code are consistent with each other. Your task is to run the [algorithm](#algorithm) step by step from a user-given step while ensuring the following (requirements)[#requirements] are met.

# Requirements

## File structure
- The specifications are provided in the #file:features/
- Put testing code into #file:tests/
- Put testing data into #file:tests/data/
- If testing variables and fixtures are shared by multiple tests, put them into #file:tests/conftest.py
- Put production code into package whose root is #file:src/ for src layout or #file:<project_name>/ for flat layout
- **!! You are not allowed to remove or modify any files outside the project directory !!**

## Code Mapping
Make sure the strict mapping of the following structure:

| Specification             | Testing Code             | Production Code         |
|---------------------------|--------------------------|-------------------------|
| features/**/*.feature     | tests/**/test_*.py       | <package root>/.../*.py |
| `Feature`                 | class                    | class                   |
| `Given` in `Background`   | fixtures                 | `__init__`              |
| `Scenario`                | testing method           | public method           |
| `Given` in `Scenario`     | code block with comment  | method arguments        |
| `When`                    | code block with comment  | method calls            |
| `Then`                    | code block with comment  | method outputs          |

Note: Methods/functions that don't correspond to any Gherkin `Scenario` **must not start its name with "test"** and should be private.

## Testing
- Use `pytest` as the testing framework, **do not use `unittest`**.
- Make sure any test is fast enough to complete within 1 minutes, by
  - adjusting hyper-parameters, settings, or configurations
  - using mock data, or split a small data from the original data that shares the distribution as similar as the one of original data
- Do not make testing file a runnable script (e.g., add `if __name__ == "__main__":`), it should be importable as a module.
- You can only have 1~2 tests for each scenario, you should merge or remove extra tests for each scenario.

## Demo
- Use jupyter notebook to demo (tools: configureNotebook, runNotebooks, readCellOutput)
- Describle correspondence between notebook sections and `Then` steps of Gherkin specifications
- Make sure outputs are meaningful enough for reviewer to check its main functionality, you should avoid null cases that are often resulted from too small scale or unproper setting   

## Development
- Code snippet: You should always run temporary code in jupyter notebooks. You are not allowed to use `python -c` or create a temporary script to run code.
- Typing hints: Annotate typing hints for all function arguments and outputs
- Package: Always use `uv` to manage virtual environments and packages, do not use `pip` directly
- Reference: Search web for documumentation and examples for unfamiliar concepts, libraries, or frameworks (tools: websearch, fetch)
- Notebook-driven development: You should actively use jupyter notebooks to explore data, inspect outputs, validate code, or debug code along with your development 

# Algorithm

You should claim the current step in the algorithm before running a step.

```pseudocode
// Step1: Setup
Setup or maintain [file structure](#file-structure)
Make sure there are at least three jupyter notebooks for temporary code execution, development, and demo

// Step2: Read specifications
Overview all specifications 
Carefully read diffs of changed ".feature" files to identify and summarize explicit and implicit expectations from the specifications (tools: changes)

// Step3: Ensure mapping
Make sure [structure mapping](#code-mapping) between specifications, testing code, and production code is followed (tools: codebase, findTestFiles, pylanceWorkspaceUserFiles, search, searchResults)
Make sure testing code coverts the explicit and implicit expectations from the specifications while following [test requirements](#testing)
Make sure production code satisfies the explicit and implicit expectations from the specifications while following [development requirements](#development)

// Debug until all tests are passed
WHILE all tests are passed IS FALSE

   // Step4: Debug
   Debug production code or testing code to fix any bugs or logical errors (tools: testFailure, configureNotebook, runNotebooks, readCellOutput)

   // Step5: Check
   Check all items of [requirements](#requirements) one by one
   Check both testing code and production code for any bugs, logical errors, and conflicts with expectations from specifications (tools: problems, pylanceSyntaxErrors, pylanceFileSyntaxErrors, pylanceImports)

   // Step6: Test
   **Import all testing files in temporary jupyter notebooks to ensure they are all importable before running tests**
   Run related tests via built-in testing tool (tools: runTests), **do not use teminal command directly**

END WHILE

// Step7: Demo
Show outputs of the generated or modified production code under instructions of [demo requirements](#demo)
```