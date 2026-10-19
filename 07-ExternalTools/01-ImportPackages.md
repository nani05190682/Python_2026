# Importing Python Packages
## Use Python Packages and Libraries

### 1. What Are Python Packages?

Python packages and libraries allow you to extend your programs without writing every feature from scratch.

For example, instead of writing your own code to download information from a website, you can use the `requests` package. Instead of implementing complex data analysis operations, you can use `pandas`.

Python provides two broad sources of functionality:

- **Standard library:** Modules included with Python. You can use them without installing separate packages.
- **Third-party packages:** Additional libraries that you typically install using `pip`.

Examples of popular third-party packages include:

| Package | Purpose |
|---|---|
| `requests` | Send HTTP requests |
| `pandas` | Analyze structured data |
| `numpy` | Perform numerical operations |
| `matplotlib` | Create charts |
| `openai` | Access OpenAI APIs |
| `python-dotenv` | Load configuration from `.env` files |

### 2. Understanding the Terminology

Before importing packages, let's understand four important terms.

**Module:** A unit of Python code, usually a `.py` file containing functions, variables, and classes.

**Package:** A way to organize related modules under a common namespace. Traditional packages commonly contain an `__init__.py` file, although namespace packages can work without one.

**Function:** A reusable block of code that performs a task, such as `print()` or `math.sqrt()`.

**Class:** A definition used to create objects. You'll explore classes later in the course.

Think of them as parts of a workshop:

- A module is like a toolbox.
- A package is like a collection of related toolboxes.
- A function is like an individual tool.
- A class is like a blueprint for creating objects.

These are simplified analogies, but they help explain how reusable Python code is organized.

### 3. Importing Modules

Python provides several ways to import functionality into your program.

#### Method 1: Import the entire module

Use `import` to make a module available under its module name.

```python
import math

result = math.sqrt(16)

print(result)
```

**Output:**

```text
4.0
```

Here:

- `import math` imports the standard-library module.
- `math.sqrt(16)` calls the square-root function.
- `result` stores the returned value.

The module name, `math`, acts as a namespace for accessing its functions and constants.

#### Method 2: Import specific functions or constants

You can import only the names you need.

```python
from math import sqrt, pi

result = sqrt(16)
circle_area = pi * 5 ** 2

print(result)
print(circle_area)
```

**Output:**

```text
4.0
78.53981633974483
```

Because you imported `sqrt` directly, you can call it without writing `math.sqrt()`.

#### Method 3: Import with an alias

An alias provides an alternative name for an imported module.

```python
import math as m

print(m.sqrt(25))
```

**Output:**

```text
5.0
```

Aliases are especially common with data analysis libraries.

```python
import pandas as pd
import numpy as np
```

Here, `pd` and `np` are widely used conventional aliases for `pandas` and `numpy`.

#### Method 4: Avoid importing everything

You may encounter this syntax:

```python
from math import *
```

This imports public names from the module into the current namespace. However, it can make it difficult to identify where a function came from and may cause naming conflicts.

Prefer explicit imports, such as:

```python
import math

print(math.sqrt(36))
```

**Best practice:** Use `import module` when you want clear namespaces, or `from module import specific_name` when importing a small number of well-known names.

### 4. Exploring Built-in Modules

Python's standard library includes many useful modules. Let's explore a few.

#### A. The `random` module

The `random` module generates pseudorandom values and selects items from sequences.

```python
import random

number = random.randint(1, 10)
fruit = random.choice(["apple", "banana", "orange"])

print("Number:", number)
print("Fruit:", fruit)
```

Example output:

```text
Number: 7
Fruit: banana
```

Your output may differ because the values are random.

- `randint(1, 10)` returns an integer between 1 and 10, inclusive.
- `choice()` selects an item from a non-empty sequence.

**Security note:** Do not use the ordinary `random` module to generate passwords, authentication tokens, or other security-sensitive random values. Use `secrets` for those purposes.

#### B. The `datetime` module

The `datetime` module helps you work with dates and times.

```python
import datetime

today = datetime.date.today()

print(today)
```

Example output:

```text
2026-10-19
```

The displayed date depends on the computer's local date when the program runs.

#### C. The `os` module

The `os` module provides operating-system-related functionality.

```python
import os

current_dir = os.getcwd()

print(current_dir)
```

Example output:

```text
/home/user/python-project
```

Your output will depend on the directory from which your program runs.

This module is useful for automation scripts that need to interact with the operating system.

#### D. The `json` module

JSON is a common format for exchanging data between applications and APIs.

```python
import json

data = {
    "name": "Alice",
    "age": 30
}

json_string = json.dumps(data)

print(json_string)
print(type(json_string))
```

**Output:**

```text
{"name": "Alice", "age": 30}
<class 'str'>
```

The `json.dumps()` function converts a Python object into a JSON-formatted string.

To convert a JSON string back into Python data:

```python
import json

json_string = '{"name": "Alice", "age": 30}'

data = json.loads(json_string)

print(data["name"])
print(data["age"])
```

**Output:**

```text
Alice
30
```

Remember:

- `json.dumps()` converts Python data into a JSON string.
- `json.loads()` parses a JSON string into Python data.

### 5. Installing External Packages

Third-party packages are typically installed using `pip`, Python's package installer.

**Important:** Activate your project's virtual environment before installing packages. This helps ensure that packages are installed into the environment used by your program.

#### Install a single package

```bash
python -m pip install requests
```

#### Install a specific version

```bash
python -m pip install requests==2.31.0
```

This requests exactly version `2.31.0`. The installation will succeed only if that version is available and compatible with your Python environment.

#### Install multiple packages

```bash
python -m pip install pandas numpy matplotlib
```

#### Verify an installation

```bash
python -m pip show requests
```

You can also test the import:

```bash
python -c "import requests; print(requests.__version__)"
```

The displayed version depends on the installed release.

#### Why use `python -m pip`?

Using `python -m pip` runs `pip` through the Python interpreter selected by the `python` command.

This helps reduce confusion when you have multiple Python installations or virtual environments.

On Windows, if `python` is not recognized, you may be able to use:

```powershell
py -m pip install requests
```

### 6. Why Virtual Environments Matter

A virtual environment isolates a project's installed packages from those of other projects.

Imagine you are working on two applications:

- Project A requires an older version of a package.
- Project B requires a newer version of the same package.

Installing everything globally can cause dependency conflicts. Separate virtual environments allow each project to maintain its own dependencies.

#### Step 1: Create a project directory

```bash
mkdir python-packages
cd python-packages
```

#### Step 2: Create a virtual environment

Windows:

```powershell
py -m venv .venv
```

Linux or macOS:

```bash
python3 -m venv .venv
```

#### Step 3: Activate it

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Linux or macOS:

```bash
source .venv/bin/activate
```

#### Step 4: Install the package

```bash
python -m pip install requests
```

#### Step 5: Run your Python program

```bash
python -c "import requests; print(requests.__version__)"
```

#### Step 6: Deactivate the environment

```bash
deactivate
```

**Recommended practice:** Use a virtual environment for each Python project, particularly when working on AI engineering, cloud automation, APIs, or data analysis.

### 7. Sharing Your Project with `requirements.txt`

When you share a Python project, other developers need to know which external packages it requires.

A common approach is to use a file called `requirements.txt`.

#### Create the file

After activating your project's virtual environment and installing the required packages, run:

```bash
python -m pip freeze > requirements.txt
```

This records the installed distributions and their versions.

Example:

```text
requests==2.32.3
```

Your actual file may contain additional dependencies and different versions.

#### Install dependencies from the file

Another developer can create and activate a virtual environment, then run:

```bash
python -m pip install -r requirements.txt
```

This tells `pip` to install the packages listed in the file.

**Important:** `pip freeze` records all installed distributions in the active environment, including transitive dependencies. For a small project, this is convenient. For larger projects, a deliberately maintained dependency list or a modern dependency manager can offer better control.

Later, you can explore `uv`, a modern Python package and project manager that supports dependency management and lockfiles.

### 8. Using External Packages

Let's explore two popular third-party packages.

#### Example A: Making HTTP requests with `requests`

Install the package:

```bash
python -m pip install requests
```

Create a Python file:

```python
import requests

url = "https://jsonplaceholder.typicode.com/todos/1"

try:
    response = requests.get(url, timeout=10)
    response.raise_for_status()

    data = response.json()

    print("Task:", data["title"])
    print("Completed:", data["completed"])

except requests.RequestException as error:
    print("Request failed:", error)
```

A typical successful response contains a task title and a Boolean value indicating whether the task is completed.

This example requires an internet connection and a reachable public API.

What the code does:

1. Imports the `requests` package.
2. Sends an HTTP GET request.
3. Sets a timeout to avoid waiting indefinitely.
4. Checks whether the HTTP response indicates failure.
5. Converts the JSON response into Python data.
6. Prints selected values.
7. Handles common request-related errors.

This pattern is useful when connecting Python programs to cloud services, monitoring systems, and AI APIs.

#### Example B: Analyzing data with `pandas`

Install the package:

```bash
python -m pip install pandas
```

Create a Python file:

```python
import pandas as pd

data = {
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 35],
    "city": ["NYC", "LA", "Chicago"]
}

df = pd.DataFrame(data)

print(df)
```

**Output:**

```text
      name  age     city
0    Alice   25      NYC
1      Bob   30       LA
2  Charlie   35  Chicago
```

A `DataFrame` is a table-like data structure containing rows and columns.

You can use `pandas` to analyze CSV files, spreadsheets, application logs, and other structured datasets.

### 9. Finding the Right Packages

When you need functionality that Python doesn't provide directly, consider these resources.

**PyPI — Python Package Index**

The primary index for Python packages. Search for package names, versions, documentation links, and project details.

Website: https://pypi.org/

**Official documentation**

Many packages have their own documentation explaining installation, supported Python versions, examples, and APIs.

**Awesome Python**

A community-maintained collection of Python frameworks, libraries, and software.

Website: https://github.com/vinta/awesome-python

**Search engines and AI assistants**

You can ask questions such as:

- "Which Python package is best for reading Excel files?"
- "Compare `requests` and `httpx`."
- "Which library should I use to build a REST API?"
- "What is the difference between `pandas` and `polars`?"

Before installing a package, check its documentation, maintenance status, compatibility, dependencies, and security considerations.

### 10. Common Mistakes

#### Mistake 1: `ModuleNotFoundError`

Example:

```python
import requests
```

If the package is not installed in the active environment, Python may report:

```text
ModuleNotFoundError: No module named 'requests'
```

Solution:

```bash
python -m pip install requests
```

If the error continues, check which interpreter is running your code:

```bash
python -c "import sys; print(sys.executable)"
```

Then install the package using that interpreter and verify that your editor or IDE is using the same environment.

#### Mistake 2: Naming your file after a package or module

Avoid naming your files:

```text
requests.py
json.py
random.py
```

These names can interfere with imports because Python may find your file instead of the intended module.

Prefer names such as:

```text
api_client_demo.py
json_parser_demo.py
random_example.py
```

If you have already used a conflicting name, rename the file and remove stale `__pycache__` files if needed.

#### Mistake 3: Installing packages globally by accident

Installing packages outside your virtual environment can lead to confusing dependency problems.

Activate the environment first and then use:

```bash
python -m pip install requests
```

#### Mistake 4: Using `from module import *`

Wildcard imports can create naming conflicts and make code harder to maintain.

Prefer:

```python
import math

print(math.sqrt(49))
```

#### Mistake 5: Assuming every package is safe

Third-party packages execute code in your environment. Install only packages you trust, and review dependencies before using them in sensitive or production systems.

### 11. Practice Exercises

Try these exercises before checking the solutions.

**Exercise 1: Use a built-in module**

Import `math` and print the square root of `144`.

**Exercise 2: Generate a random number**

Use `random.randint()` to generate an integer between `1` and `100`.

**Exercise 3: Work with JSON**

Create a Python dictionary containing a user's name and age. Convert it to a JSON string using `json.dumps()`.

**Exercise 4: Install an external package**

Create and activate a virtual environment, install `requests`, and check its version.

**Exercise 5: Call an API**

Use `requests` to fetch the following resource:

`https://jsonplaceholder.typicode.com/todos/1`

Print the HTTP status code and the task title.

**Exercise 6: Use pandas**

Create a `pandas.DataFrame` containing three employees, their departments, and their experience in years. Print the resulting table.

### 12. Sample Solutions

#### Solution 1

```python
import math

print(math.sqrt(144))
```

Output:

```text
12.0
```

#### Solution 2

```python
import random

number = random.randint(1, 100)

print(number)
```

The output varies each time you run the program.

#### Solution 3

```python
import json

user = {
    "name": "Alice",
    "age": 30
}

json_string = json.dumps(user)

print(json_string)
```

Output:

```text
{"name": "Alice", "age": 30}
```

#### Solution 4

After activating your virtual environment:

```bash
python -m pip install requests
python -c "import requests; print(requests.__version__)"
```

#### Solution 5

```python
import requests

response = requests.get(
    "https://jsonplaceholder.typicode.com/todos/1",
    timeout=10
)

response.raise_for_status()

data = response.json()

print("Status:", response.status_code)
print("Title:", data["title"])
```

This exercise requires internet access and a reachable API.

#### Solution 6

```python
import pandas as pd

data = {
    "name": ["Alice", "Bob", "Charlie"],
    "department": ["DevOps", "Development", "Testing"],
    "experience": [5, 3, 7]
}

df = pd.DataFrame(data)

print(df)
```

### 13. Quick Summary

| Concept | Example | Purpose |
|---|---|---|
| Import a module | `import math` | Access module functionality |
| Import specific names | `from math import sqrt` | Use selected names directly |
| Import with an alias | `import pandas as pd` | Use a shorter module name |
| Install a package | `python -m pip install requests` | Add third-party functionality |
| Create an environment | `python -m venv .venv` | Isolate project dependencies |
| Save dependencies | `python -m pip freeze > requirements.txt` | Record installed versions |
| Install dependencies | `python -m pip install -r requirements.txt` | Install listed packages |
| Make an HTTP request | `requests.get(url)` | Retrieve data from a service |
| Create a DataFrame | `pd.DataFrame(data)` | Organize data into rows and columns |

**Key takeaway:** Importing packages gives your Python programs access to reusable functionality. Learn the import patterns, use virtual environments, manage dependencies carefully, and select packages based on your project's requirements.

### What's Next?

**Working with APIs — Fetch Data from the Internet**

You'll learn how HTTP requests work, how to send GET requests, how to handle status codes and errors, and how to process JSON responses from external services.
