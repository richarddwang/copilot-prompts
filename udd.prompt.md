---
mode: agent
description: How-to guides Driven Development. Generate or modify testing code and production code based on the how-to guides.
---

Your task is to execute Usage driven development (UDD). You should follow the requirements below strictly during your development, and implement all implicit and explicit expectations in the how-to guides #file:USAGE.md, until you pass tests related to your modifications. After related tests passed, you will give report for your modifications with simple demo for the main features or usage through jupyter notebook.

# Testing
- Cover explicit and implicit expectation: Write test cases for both explicit expectations from code examples and implicit expectations hidden in the description in how-to guides.
- Framework: `pytest` but not `unittest`
- Directory structure: Put testing code under `tests/`, mocking data (if needed) under `tests/data/`, fixtures and variables used by different test modules under `tests/conftest.py`
- Speed: fast, best within 1 minute, and avoid long-running tests
- File manipulation: use `tempfile` module to create temporary files and directories for testing file operations, and ensure they are cleaned up after tests. **!! You are not allowed to remove or modify any files outside the project directory or /tmp !!**
- Start tests with built-in tool: **always use VSCode built-in testing tools to invoke tests, never use command line to invoke tests**
- Simplicity: Keep testing code simple and easy to understand and maintain. For example, prefer testing function over testing class.
- Check before testing: make sure the code to be tested has no problems and comply with all of our requirements before invoking the corresponding test cases.

# Package management
- Framework: use `uv` but not `pip`



# Development practices
- Jupyter notebook driven development: Instead of directly write or debug code, explore or debug code, data, and files in various notebooks, then move the code to .py files.
- Search

# Demo
- Create a `demos/` directory to store demo jupyter notebooks
- Showcase the main features or usage of the modified code this time. 
- The demo should be simple and easy to understand, avoid complex scenarios or edge cases. So reviewers can quickly grasp the main idea and usage of the modified code.