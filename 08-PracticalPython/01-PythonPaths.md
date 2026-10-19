# Python Paths
## Understanding How Python Finds Files

### 1. Why are paths confusing?

When you start working with multiple Python files, you will eventually encounter errors such as:

```text
FileNotFoundError: No such file or directory
```

or

```text
ModuleNotFoundError: No module named 'helper'
```

These errors often occur because Python cannot find the file or module you want to use.

Don't worry! Understanding paths takes practice. Once you understand where Python looks for files and modules, these errors become much easier to troubleshoot.

In this lesson, you will learn:

- What a file path is.
- The difference between the current working directory and the script directory.
- How to access files in the same folder, subfolders, and parent folders.
- How Python finds modules when you use `import`.
- How to troubleshoot common path errors.

### 2. Understand the basic project structure

Imagine you have a project named `my-project`:

```text
my-project/
├── script.py
├── data.txt
├── config.json
└── folder/
    ├── other.txt
    └── helper.py
```

Here:

- `script.py` is your main Python program.
- `data.txt` contains input data.
- `config.json` contains configuration settings.
- `folder/` is a subfolder.
- `other.txt` is a file inside that subfolder.
- `helper.py` contains reusable Python code.

Before accessing any file, ask yourself two questions:

1. **Where is my Python program running from?**
2. **Where is the file or module I want to access?**

These two questions will help you determine the correct path.

### 3. Understand the current working directory

The **current working directory (CWD)** is the directory from which your Python process is operating.

Check it using `os.getcwd()`:

```python
import os

print("Current working directory:", os.getcwd())
```

Example output:

```text
Current working directory: /Users/student/my-project
```

Your actual output depends on your computer and how you launch Python.

The current working directory is important because a relative file path such as `"data.txt"` is normally resolved from that directory.

**Important distinction:** The current working directory is not necessarily the folder containing your Python script. For example, if you run a script using an absolute path from another directory, the working directory can remain unchanged.

### 4. Understand relative and absolute paths

There are two common types of file paths.

**Relative path:** Specifies a location relative to a directory, typically the current working directory when opening a file.

Examples:

```python
"data.txt"
"folder/other.txt"
"../config.json"
```

**Absolute path:** Specifies the full path to a file or directory.

Examples:

```text
Windows:
C:\Users\student\my-project\data.txt

macOS or Linux:
/Users/student/my-project/data.txt
```

Absolute paths identify a specific location. Relative paths are usually more portable when shared within a project.

### 5. Navigate between folders

Let's use this directory structure:

```text
my-project/
├── script.py
├── data.txt
├── config.json
└── folder/
    └── other.txt
```

Assume the current working directory is `my-project`.

#### Access a file in the same folder

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

The path `"data.txt"` points to the file in the current working directory.

#### Access a file inside a subfolder

```python
with open("folder/other.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

The forward slash separates the folder name from the filename.

#### Access a file in the parent folder

The notation `..` means the parent directory.

For example:

```python
with open("../config.json", "r", encoding="utf-8") as file:
    content = file.read()
```

This looks for `config.json` one directory above the current working directory.

The path must correspond to the actual directory structure. If the file does not exist there, Python raises `FileNotFoundError`.

### 6. Use `pathlib` for reliable file paths

Python provides a built-in module called `pathlib` for working with file and directory paths.

It is often easier to read than manually combining strings.

```python
from pathlib import Path

# Start from the current working directory
project_dir = Path.cwd()

# Build paths
data_file = project_dir / "data.txt"
nested_file = project_dir / "folder" / "other.txt"

print("Project directory:", project_dir)
print("Data file:", data_file)
print("Data file exists:", data_file.exists())
print("Nested file exists:", nested_file.exists())
```

The `/` operator joins path components when used with `Path` objects.

For example:

```python
data_file = project_dir / "data" / "sales.csv"
```

This creates a path equivalent to `data/sales.csv` inside `project_dir`.

`pathlib` automatically handles the appropriate path conventions for the operating system.

### 7. Find paths relative to your Python script

Sometimes you want to locate files relative to the script itself, regardless of the current working directory.

Use `__file__`:

```python
from pathlib import Path

# Locate the folder containing this Python script
script_dir = Path(__file__).resolve().parent

# Build a path relative to the script
data_file = script_dir / "data" / "sales.csv"

print("Script directory:", script_dir)
print("Data file:", data_file)
print("File exists:", data_file.exists())
```

Suppose your project is organized like this:

```text
sales-analysis/
├── analyzer.py
└── data/
    └── sales.csv
```

If the code above is in `analyzer.py`, it constructs the path to `data/sales.csv` relative to the script's location.

This is often more reliable than assuming the current working directory is always the project directory.

Note that `__file__` is normally available when Python runs a script as a file. Some interactive environments may not define it.

### 8. Files and modules are different

Python handles regular files and Python modules differently.

**Regular files** contain data, such as CSV, TXT, and JSON files. You typically access them using `open()`, pandas, or another file-reading library.

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()
```

**Python modules** contain Python code. You typically access them using `import` statements.

Suppose you have:

```text
my-project/
├── main.py
└── helper.py
```

Inside `helper.py`:

```python
def greet(name):
    return f"Hello, {name}!"
```

Inside `main.py`:

```python
from helper import greet

print(greet("Python"))
```

When the project is launched in the usual way, Python can generally import `helper` because it is alongside the main script.

Expected output:

```text
Hello, Python!
```

You do not use `open()` to import Python code. Likewise, `import` is not the normal way to read CSV or text data.

### 9. Import modules from subfolders

Consider this project:

```text
my-project/
├── main.py
└── utils/
    ├── __init__.py
    └── helper.py
```

Inside `utils/helper.py`:

```python
def add(a, b):
    return a + b
```

Inside `main.py`:

```python
from utils.helper import add

print(add(10, 20))
```

Output:

```text
30
```

Here:

- `utils` is the package directory.
- `helper` is the module.
- `add` is the function.

Notice that imports use dots rather than filesystem slashes.

```python
from utils.helper import add
```

This is different from a file path such as:

```python
"utils/helper.py"
```

The `__init__.py` file explicitly marks `utils` as a regular Python package. Modern Python also supports namespace packages without `__init__.py` in suitable situations, but using the file is a clear approach for beginner projects.

### 10. How Python finds modules

When you use an import statement, Python searches for modules through its import system. One important part of that system is `sys.path`, a list of locations used to find modules.

Inspect it:

```python
import sys

for path in sys.path:
    print(path)
```

The output varies by environment, but commonly includes locations such as:

- The script directory or another startup-dependent import location.
- Python's standard library directories.
- Installed third-party package directories.
- Additional locations configured by the environment.

This explains why you can import packages such as `json`, `pathlib`, or `requests` without specifying a filesystem path in the import statement.

The important distinction is:

- **File access:** A relative path is generally resolved from the current working directory.
- **Module imports:** Python searches locations defined by its import system, including `sys.path`.

These mechanisms are related to the filesystem but are not interchangeable.

### 11. What if you need to import from a parent folder?

Suppose your project looks like this:

```text
workspace/
├── shared_utils.py
└── sales-analysis/
    └── analyzer.py
```

If you run `analyzer.py` directly, Python may not automatically find `shared_utils.py`, because the parent directory is not necessarily on the import search path.

You might see:

```text
ModuleNotFoundError: No module named 'shared_utils'
```

For a quick experiment, you can add the parent directory to `sys.path`:

```python
import sys
from pathlib import Path

script_dir = Path(__file__).resolve().parent
parent_dir = script_dir.parent

sys.path.insert(0, str(parent_dir))

import shared_utils
```

This works by adding the parent directory to Python's module search path.

However, modifying `sys.path` manually is generally not the best long-term solution for a growing application. It can make imports dependent on execution details and can cause module-name conflicts.

**Better practice for larger projects:** Organize reusable code into packages and run the application from the project root, or install your project as a package in a virtual environment.

For example:

```text
workspace/
└── sales-analysis/
    ├── pyproject.toml
    └── src/
        └── sales_analysis/
            ├── __init__.py
            └── analyzer.py
```

This structure is more suitable when your application grows beyond a few scripts.

### 12. Common path errors and how to fix them

| Error | Common cause | What to check |
|---|---|---|
| `FileNotFoundError` | A data file cannot be found at the specified path. | Check the working directory, filename, and directory structure. |
| `ModuleNotFoundError` | Python cannot find the requested module. | Check the import name, package structure, interpreter, and `sys.path`. |
| Wrong file is loaded | A relative path points to a different file with the same name. | Print the resolved path before opening the file. |
| Works in terminal but not in VS Code | The working directory or interpreter differs. | Check the selected interpreter and `os.getcwd()`. |
| Import works in one folder but not another | The import depends on how the program was launched. | Use a consistent project layout and import strategy. |

To debug a missing file, try:

```python
from pathlib import Path

file_path = Path("data/sales.csv").resolve()

print("Looking for:", file_path)
print("Exists:", file_path.exists())
```

This shows the exact location Python is checking after resolving the relative path.

On Windows, macOS, and Linux, `pathlib` is preferable to manually building paths with backslashes. Forward slashes are also accepted by Python for many Windows file paths, but `pathlib` avoids unnecessary platform-specific handling.

### 13. Practice exercises

**Exercise 1: Check your working directory**

Write a program that prints the current working directory.

**Exercise 2: Find a data file**

Use `pathlib` to check whether `data/sales.csv` exists relative to your current working directory.

**Exercise 3: Find a file relative to the script**

Rewrite Exercise 2 using `Path(__file__).resolve().parent`.

**Exercise 4: Import a helper function**

Create `helper.py` with a function that multiplies two numbers. Import and call the function from `main.py`.

**Exercise 5: Diagnose an error**

Change a valid filename to a filename that does not exist. Print the resolved path and determine why the file cannot be found.

### 14. Lesson summary

In this lesson, you learned:

- The difference between relative and absolute paths.
- How to check the current working directory with `os.getcwd()`.
- How to navigate into subfolders and parent directories.
- How to build paths with `pathlib`.
- How to create paths relative to a script using `__file__`.
- How Python imports modules and searches `sys.path`.
- Why file paths and module imports work differently.
- How to troubleshoot common path errors.

**Remember this mental model:**

1. Identify the location of your file or script.
2. Decide whether you need to access a data file or import Python code.
3. Use `pathlib` to build reliable file paths.
4. Use Python's import system to locate modules.
5. Print the resolved path or inspect `sys.path` when something goes wrong.

You do not need to memorize every detail immediately. Practice these patterns, and file paths will become much easier to understand.

**Next lesson: Working with Files — Read, Write, and Manage Data in Python.**
