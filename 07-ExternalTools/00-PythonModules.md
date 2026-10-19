# Python Modules and Packages
## Extend Python with External Libraries

### 1. Beyond Built-in Python

Python provides built-in functions such as `print()`, `len()`, and `type()`. However, when you want to perform more advanced tasks, you often need additional functionality.

For example:

- Download data from websites.
- Read and analyze Excel files.
- Connect to REST APIs.
- Build AI-powered applications.
- Automate repetitive tasks.
- Store configuration securely outside your source code.

You don't need to write everything from scratch. Python has a large ecosystem of reusable code that you can import and use in your projects.

### 2. What Are Modules, Packages, and Libraries?

These terms are related, but they have slightly different meanings.

**Module:** A Python file containing reusable code, such as functions, variables, and classes.

**Package:** A way to organize related Python modules under a common namespace. Traditional Python packages typically contain an `__init__.py` file, although Python also supports namespace packages without one.

**Library:** A general term for reusable code that provides functionality for other programs. A library may contain multiple modules and packages.

Think of them like this:

- A module is like one toolbox.
- A package is like a collection of related toolboxes.
- A library is a reusable collection of functionality that helps you complete a task.

Python terminology can overlap, and developers sometimes use the word *library* informally to describe a package.

### 3. Two Types of Modules and Packages

For beginners, it's useful to distinguish between functionality included with Python and third-party packages that you install separately.

#### A. Python standard library

The standard library comes with Python and provides many useful modules.

Examples include:

| Module | Purpose |
|---|---|
| `math` | Mathematical operations |
| `random` | Random number generation |
| `datetime` | Dates and times |
| `os` | Operating-system interactions |
| `json` | Working with JSON data |
| `pathlib` | Working with filesystem paths |
| `statistics` | Basic statistical calculations |

Example:

```python
import math

print(math.sqrt(25))
print(math.pi)
```

Output:

```text
5.0
3.141592653589793
```

You can use these modules without installing a third-party package.

#### B. Third-party packages

Third-party packages are developed and distributed separately from Python itself. You can usually install them using `pip`, Python's package installer.

Examples include:

| Package | Purpose |
|---|---|
| `requests` | Making HTTP requests |
| `pandas` | Data analysis and tabular data |
| `beautifulsoup4` | Parsing HTML and XML |
| `openai` | Accessing OpenAI APIs |
| `python-dotenv` | Loading configuration from `.env` files |
| `fastapi` | Building APIs |
| `pytest` | Testing Python code |

Many third-party packages are published on the Python Package Index (PyPI).

### 4. Importing Modules

Before using functionality from a module, you generally import it.

#### Method 1: Import the entire module

```python
import math

result = math.sqrt(64)

print(result)
```

Output:

```text
8.0
```

Here, `import math` makes the `math` module available, and `math.sqrt()` calls its square-root function.

#### Method 2: Import a specific function

```python
from math import sqrt

result = sqrt(81)

print(result)
```

Output:

```text
9.0
```

You can call `sqrt()` directly because you imported that function specifically.

#### Method 3: Import with an alias

You can assign a shorter name using `as`.

```python
import math as m

print(m.factorial(5))
```

Output:

```text
120
```

This can be convenient when a module has a long name. Some popular libraries also use established aliases, such as `import pandas as pd`.

#### Best practice

Avoid `from module import *` in most application code. It can make it unclear where a name came from and can cause naming conflicts.

### 5. Understanding How Imports Work

When you import a module, Python locates it using its import system and makes its names available to your program.

For example:

```python
import datetime

today = datetime.date.today()

print(today)
```

The output is the current date on the computer where the program runs, so it will vary.

In this example:

1. `import datetime` imports the standard-library module.
2. `datetime.date.today()` obtains the current local date.
3. `today` stores the returned date object.
4. `print(today)` displays the date.

**Important:** The name used in an import is not always identical to the package name used during installation. For example, you install `beautifulsoup4` but import `bs4`.

### 6. Installing External Packages with `pip`

Let's install the `requests` package, which is commonly used to make HTTP requests.

Open your terminal or PowerShell and run:

```bash
python -m pip install requests
```

On Windows, if `python` is not recognized, try:

```powershell
py -m pip install requests
```

Using `python -m pip` helps ensure that `pip` runs through the Python interpreter you selected.

#### Verify the installation

Run:

```bash
python -m pip show requests
```

This displays package information, including its installed version and location.

You can also verify it from Python:

```python
import requests

print(requests.__version__)
```

The version number depends on the installed release.

#### Why do we use `pip`?

`pip` is used to install, upgrade, and uninstall Python packages.

Examples:

```bash
python -m pip install requests
python -m pip install --upgrade requests
python -m pip uninstall requests
```

Use the appropriate Python interpreter when running these commands, especially if you have multiple Python installations.

### 7. Using a Virtual Environment

A virtual environment creates an isolated Python environment for a project. This helps prevent package dependencies from different projects from interfering with each other.

For example, one project may require one version of a library while another project requires a different version.

#### Step 1: Create a project directory

```bash
mkdir python-packages
cd python-packages
```

#### Step 2: Create a virtual environment

On Windows:

```powershell
py -m venv .venv
```

On Linux or macOS:

```bash
python3 -m venv .venv
```

#### Step 3: Activate the environment

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

Linux or macOS:

```bash
source .venv/bin/activate
```

#### Step 4: Install a package

```bash
python -m pip install requests
```

The package is installed into the active virtual environment rather than being intentionally shared with every Python project.

#### Step 5: Deactivate the environment

When you finish working, run:

```bash
deactivate
```

**Recommended practice:** Create a virtual environment for each Python project, particularly when building automation tools, APIs, or AI applications.

### 8. Package Example: Making an HTTP Request

Let's use `requests` to access a public API and retrieve JSON data.

First, install the package:

```bash
python -m pip install requests
```

Then create a file named `api_example.py`:

```python
import requests

url = "https://jsonplaceholder.typicode.com/todos/1"

response = requests.get(url, timeout=10)

response.raise_for_status()

data = response.json()

print(data)
print("Task:", data["title"])
print("Completed:", data["completed"])
```

The example uses a public demonstration API. It requires an internet connection and the service to be reachable.

A typical response contains fields similar to these:

```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

The exact response depends on the API.

Let's understand the code:

- `import requests` imports the package.
- `requests.get()` sends an HTTP GET request.
- `timeout=10` limits how long the request waits for a response.
- `raise_for_status()` raises an exception if the HTTP response indicates an unsuccessful status.
- `response.json()` parses the JSON response into Python data structures.
- `data["title"]` retrieves the task title from the dictionary.

This is a foundational technique for working with cloud services, monitoring platforms, and AI APIs.

### 9. Popular Packages for Python Developers

As you progress, you'll encounter packages designed for different types of work.

#### Web APIs and HTTP

- `requests` — a straightforward HTTP client.
- `httpx` — an HTTP client that supports synchronous and asynchronous requests.
- `fastapi` — a framework for building APIs.

#### Data analysis

- `pandas` — works with tables, CSV files, and structured data.
- `numpy` — provides numerical arrays and mathematical operations.
- `openpyxl` — reads and writes Excel `.xlsx` files.

#### Web scraping

- `beautifulsoup4` — extracts information from HTML and XML documents.
- `scrapy` — a framework for building web crawlers.

Always respect website terms, access controls, and applicable privacy requirements when collecting web data.

#### AI engineering

- `openai` — provides an SDK for accessing OpenAI APIs.
- `transformers` — provides tools for working with transformer-based machine learning models.
- `langchain` — provides components for building applications with language models.
- `langgraph` — supports stateful, multi-step agent workflows.

These packages have different purposes and requirements. Choose them based on your project rather than installing everything at once.

### 10. Handling Packages and Secrets Safely

Installing a package gives your program access to additional code, so you should consider security and configuration.

**Good practices:**

1. Install packages from trusted sources.
2. Review package documentation and maintenance status.
3. Use virtual environments.
4. Pin or lock dependency versions when reproducibility matters.
5. Avoid installing unnecessary packages.
6. Keep API keys and passwords out of source code.
7. Avoid running installation commands with elevated privileges unless required and understood.

For example, `python-dotenv` can load configuration from a `.env` file.

Install it:

```bash
python -m pip install python-dotenv
```

Create a `.env` file:

```text
APP_ENV=development
API_KEY=replace_with_your_key
```

Load the values in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()

environment = os.getenv("APP_ENV")
api_key = os.getenv("API_KEY")

print("Environment:", environment)
print("API key configured:", bool(api_key))
```

Output:

```text
Environment: development
API key configured: True
```

The example deliberately does not print the API key itself.

**Security reminder:** Do not commit `.env` files containing real secrets to Git. Add `.env` to your `.gitignore` file and use a suitable secret manager for production applications.

### 11. Common Mistakes

#### Mistake 1: Installing a package into the wrong Python environment

You may install a package successfully but receive `ModuleNotFoundError` when running your program with another interpreter.

Check which Python interpreter is being used:

```bash
python -c "import sys; print(sys.executable)"
```

Install the package using that same interpreter:

```bash
python -m pip install requests
```

In VS Code, select the intended Python interpreter and activate the correct virtual environment.

#### Mistake 2: Confusing package names with import names

For example:

```bash
python -m pip install beautifulsoup4
```

But in Python:

```python
from bs4 import BeautifulSoup
```

The installation name and import name can differ.

#### Mistake 3: Naming your file after a module

Avoid naming your own Python file `requests.py`, `json.py`, or `random.py`.

These names can interfere with Python's ability to import the intended module.

Prefer names such as:

- `api_client.py`
- `json_parser_demo.py`
- `random_number_demo.py`

If you already created a conflicting filename, rename it and remove any related stale `__pycache__` files if necessary.

#### Mistake 4: Forgetting network or API errors

External services may be unavailable, slow, or return unsuccessful responses. Use timeouts and handle errors appropriately in production code.

```python
import requests

try:
    response = requests.get(
        "https://jsonplaceholder.typicode.com/todos/1",
        timeout=10
    )
    response.raise_for_status()
    print(response.json())

except requests.RequestException as error:
    print("Request failed:", error)
```

This example handles common request-related failures without crashing due to an uncaught request exception.

### 12. Practice Exercises

Try these exercises before checking the solutions.

**Exercise 1: Import a built-in module**

Import `math` and display the square root of `144`.

**Exercise 2: Work with dates**

Import `datetime` and display today's date.

**Exercise 3: Install an external package**

Create a virtual environment and install `requests` inside it. Verify the installation using `python -m pip show requests`.

**Exercise 4: Make an API request**

Use `requests` to send a GET request to:

`https://jsonplaceholder.typicode.com/todos/1`

Print the HTTP status code and the response's `title` field.

**Exercise 5: Load environment variables**

Install `python-dotenv`, create a `.env` file containing `APP_ENV=development`, and print the value from Python.

### 13. Sample Solutions

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
import datetime

print(datetime.date.today())
```

The output depends on the current date on your computer.

#### Solution 3

Create and activate a virtual environment using the commands in Section 7, then run:

```bash
python -m pip install requests
python -m pip show requests
```

#### Solution 4

```python
import requests

response = requests.get(
    "https://jsonplaceholder.typicode.com/todos/1",
    timeout=10
)

response.raise_for_status()

data = response.json()

print("Status code:", response.status_code)
print("Title:", data["title"])
```

This exercise requires an internet connection and a reachable API.

#### Solution 5

Install the package:

```bash
python -m pip install python-dotenv
```

Create `.env`:

```text
APP_ENV=development
```

Python code:

```python
import os
from dotenv import load_dotenv

load_dotenv()

print(os.getenv("APP_ENV"))
```

Output:

```text
development
```

### 14. Quick Summary

| Concept | Purpose |
|---|---|
| Module | A Python file containing reusable code |
| Package | A way to organize related Python modules |
| Standard library | Modules included with Python |
| Third-party package | Additional functionality installed separately |
| `import` | Makes module functionality available |
| `pip` | Installs and manages Python packages |
| Virtual environment | Isolates project dependencies |
| `requests` | Sends HTTP requests |
| `python-dotenv` | Loads environment variables from `.env` files |

**Key takeaway:** Python packages allow you to extend your programs without implementing every capability from scratch. Learn to import modules, install packages into the correct environment, and use external libraries safely.

### What's Next?

**Working with APIs and JSON — Connect Python to External Services**

You'll learn how Python communicates with APIs, sends HTTP requests, and processes JSON responses. These skills are essential for cloud automation, monitoring, and AI engineering.
