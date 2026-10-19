# Packages and pip: Understanding Python’s Package Ecosystem

## 1. Introduction: Building on Existing Code

One of Python’s greatest strengths is its extensive ecosystem of packages and libraries.

Instead of writing every feature from scratch, you can reuse code developed and maintained by other programmers. These packages help you solve problems faster, reduce repetitive work, and build applications more efficiently.

For example, rather than implementing every detail of HTTP communication yourself, you can use a package such as `requests` to communicate with web services.

## 2. What Are Python Packages?

A Python package is a collection of reusable Python modules that provide specific functionality.

Different packages are designed for different tasks.

| Package | Purpose |
|---|---|
| `requests` | Send HTTP requests and communicate with web services |
| `pandas` | Analyze and manipulate tabular data |
| `numpy` | Perform numerical calculations and array operations |
| `openai` | Integrate applications with OpenAI APIs |
| `beautifulsoup4` | Parse HTML and XML documents |

Think of each package as a toolbox containing specialized tools for a particular job.

By combining packages, you can build applications without implementing every component yourself.

## 3. Meet pip: Python’s Package Installer

`pip` is the standard package installer commonly used to install Python packages from the Python Package Index (PyPI) and other package repositories.

It allows you to:

- Download and install packages.
- Install specific package versions.
- Install dependencies required by other packages.
- Upgrade existing packages.
- Uninstall packages that are no longer needed.

You can check whether pip is available by running:

```bash
python -m pip --version
```

On Windows, you can also use:

```powershell
py -m pip --version
```

On macOS or Linux, you may need:

```bash
python3 -m pip --version
```

A compatible Python installation commonly includes pip. If it is missing, it may need to be installed or enabled separately.

**Best practice:** Use `python -m pip` instead of just `pip`. This helps ensure that packages are managed using the Python interpreter you intended to use.

## 4. Open the VS Code Integrated Terminal

Before installing packages, open your `python-for-ai` project in Visual Studio Code.

Follow these steps:

1. Open your project folder in VS Code.
2. Select **Terminal → New Terminal**.
3. Check whether your virtual environment is active.

An activated environment may display a prompt similar to this:

```text
(.venv) PS C:\Users\YourName\Documents\PythonProjects\python-for-ai>
```

The `(.venv)` prefix indicates that the virtual environment is active in that terminal.

If your environment is not active, activate it manually.

**Windows PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
source .venv/bin/activate
```

Once activated, packages installed through that environment's Python interpreter will normally be installed into its package directory rather than the base environment.

## 5. Install Your First Python Package

Let's install the `requests` package, which is commonly used to send HTTP requests.

Run the following command in your activated terminal:

```bash
python -m pip install requests
```

Wait for the installation to complete.

You should see a success message indicating that `requests` and any required dependencies have been installed.

The exact package versions and terminal output may differ from one installation to another.

### What Happens During Installation?

When you execute the installation command:

1. pip searches the configured package repository, typically PyPI.
2. It identifies a compatible package distribution.
3. It downloads the package and any required dependencies that are not already installed.
4. It installs them into the active Python environment.
5. It reports whether the installation succeeded.

The package files are typically stored in a directory such as:

**Windows:**

```text
.venv\Lib\site-packages\requests\
```

**macOS/Linux:**

```text
.venv/lib/python3.x/site-packages/requests/
```

Here, `python3.x` represents the relevant Python version directory; the exact path varies by environment and operating system.

You normally do not need to modify these files manually.

## 6. Use an Installed Package in Your Python Program

Now that `requests` is installed, let's use it in a Python program.

Create a file named `api_example.py` in your project folder.

Add the following code:

```python
import requests

# Send an HTTP GET request to the GitHub API
response = requests.get(
    "https://api.github.com",
    timeout=10
)

# Display the HTTP status code
print("Status code:", response.status_code)
```

Save the file and run:

```bash
python api_example.py
```

If the request succeeds, you will typically see:

```text
Status code: 200
```

A status code of `200` means the HTTP request succeeded.

**Note:** This example requires an internet connection. Network restrictions, server availability, or request failures may produce different results.

### Understanding the Code

- `import requests` makes the installed package available to your program.
- `requests.get()` sends an HTTP GET request to the specified URL.
- `timeout=10` limits how long the request waits before timing out.
- `response.status_code` retrieves the HTTP status code returned by the server.
- `print()` displays the result in the terminal.

Using a package allows you to perform common HTTP operations without implementing the low-level networking details yourself.

## 7. List Installed Packages

You can inspect the packages installed in your current environment.

Run:

```bash
python -m pip list
```

Example output:

```text
Package             Version
------------------- -------
certifi             ...
charset-normalizer  ...
idna                ...
pip                 ...
requests            ...
urllib3             ...
```

The versions and package list will depend on your environment.

Notice that installing `requests` may also install dependencies such as `urllib3`, `certifi`, `idna`, and `charset-normalizer`.

pip resolves and installs the required dependencies automatically when possible.

### View Details About a Package

To inspect the installed version and package information, run:

```bash
python -m pip show requests
```

This command displays details such as the package version, installation location, and dependencies.

## 8. Install Specific Package Versions

Sometimes a project requires a particular package version for compatibility or reproducibility.

pip supports version specifiers for this purpose.

### Install an Exact Version

```bash
python -m pip install "requests==2.30.0"
```

This requests version `2.30.0`.

### Install a Minimum Version

```bash
python -m pip install "requests>=2.28.0"
```

This requests version `2.28.0` or later, subject to other constraints and compatibility requirements.

### Install a Compatible Version

```bash
python -m pip install "requests~=2.31.0"
```

This allows versions compatible with the `2.31` release series, normally starting at `2.31.0` and below `2.32.0`.

**Important:** These commands demonstrate version syntax. When working on a real project, check the project's compatibility requirements before changing an installed package version.

## 9. Upgrade and Uninstall Packages

### Upgrade a Package

To upgrade `requests` to a newer version permitted by the applicable constraints, run:

```bash
python -m pip install --upgrade requests
```

### Uninstall a Package

If you no longer need a package, run:

```bash
python -m pip uninstall requests
```

pip normally asks you to confirm the removal before proceeding.

### Verify the Result

After installation, upgrading, or uninstalling, you can check the current package list:

```bash
python -m pip list
```

## 10. Where Do Python Packages Come From?

The Python Package Index (PyPI) is the main public repository used by pip to discover and download Python packages.

Official website: https://pypi.org/

Developers publish packages there so other people can install and reuse their code.

However, not every package on PyPI is trustworthy or well maintained. Before installing an unfamiliar package, review its documentation, maintainer information, release history, and security considerations.

For professional projects, use trusted sources and avoid installing packages unnecessarily.

## 11. Common pip Errors and Solutions

### Error 1: `pip` Is Not Recognized

Instead of running:

```bash
pip install requests
```

Use:

```bash
python -m pip install requests
```

If `python` is unavailable, try the appropriate launcher for your operating system.

### Error 2: Permission Denied

A permission error may occur when you try to install packages into a protected system Python installation.

For a project, create and activate a virtual environment, then install the package inside it.

```bash
python -m venv .venv
```

Activate the environment using the appropriate command for your operating system, then run:

```bash
python -m pip install requests
```

### Error 3: No Matching Distribution Found

This error may occur when:

- The requested version does not exist.
- The package does not support your Python version.
- Your operating system or architecture is incompatible with the available distributions.
- The configured package repository cannot provide a compatible release.

Check the package documentation and your Python version, then choose a compatible release.

### Error 4: Module Not Found

If Python reports:

```text
ModuleNotFoundError: No module named 'requests'
```

Check whether the package is installed in the same environment used to execute your script.

Run:

```bash
python -m pip show requests
python -c "import sys; print(sys.executable)"
```

If necessary, select the correct interpreter in VS Code and install the package into that environment.

## 12. Best Practices for Package Management

Follow these recommendations when developing Python projects:

1. Create a separate virtual environment for each project.
2. Install packages using `python -m pip`.
3. Check package documentation before selecting versions.
4. Avoid installing unnecessary packages.
5. Record project dependencies in a `requirements.txt` file when appropriate.
6. Do not commit your `.venv` directory to Git.
7. Review unfamiliar packages before installing them.

To record the current environment's installed package versions, run:

```bash
python -m pip freeze > requirements.txt
```

To install the recorded dependencies in another environment, run:

```bash
python -m pip install -r requirements.txt
```

## 13. Lesson Summary

In this lesson, you learned:

- What Python packages are and why they are useful.
- How pip installs and manages packages.
- How to install and import `requests`.
- How to list, inspect, upgrade, and uninstall packages.
- How to install specific package versions.
- How to identify and troubleshoot common installation errors.
- Why virtual environments and dependency management are important.

## 14. Practice Exercise

Create a file named `package_practice.py` and complete the following tasks:

1. Import the `requests` package.
2. Send a GET request to `https://api.github.com`.
3. Set a timeout of 10 seconds.
4. Print the HTTP status code.
5. Print whether the request succeeded using `response.ok`.

Starter code:

```python
import requests

response = requests.get(
    "https://api.github.com",
    timeout=10
)

print("Status code:", response.status_code)
print("Request successful:", response.ok)
```

Run your program and verify the output.

**Next lesson: Interactive Python — Exploring Python in the Interpreter.**
