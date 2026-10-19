# Python Environment: Understanding Virtual Environments

**Lesson: Virtual Environments — Keep Your Python Projects Organized**

## 1. Understanding Your Python Installation

When you install Python, it is stored in a directory on your computer. The location depends on your operating system and installation method.

Common examples include:

- **Windows:** `C:\Users\<YourName>\AppData\Local\Programs\Python\Python313\`
- **macOS:** `/Library/Frameworks/Python.framework/Versions/3.13/`
- **Linux:** `/usr/bin/python3`

These paths are examples; your actual Python installation may be located elsewhere.

The Python interpreter is the program that executes your Python code. You can use the same interpreter for multiple projects, but installing every project's packages into one shared environment can cause dependency conflicts.

## 2. Why Do We Need Virtual Environments?

Imagine that you are working on two Python projects.

- **Project A** requires version 1.0 of a particular package.
- **Project B** requires version 2.0 of the same package.

If both projects use the same Python environment, installing or upgrading the package for Project B may cause Project A to stop working correctly.

This problem is known as a **dependency conflict**.

Virtual environments help prevent this by providing separate package installations for different projects.

## 3. What Is a Virtual Environment?

A Python virtual environment is an isolated environment that has its own package installation directory and Python executable reference.

Think of it as a separate workspace for each Python project.

A virtual environment provides:

- **Package isolation:** Each project can use its own package versions.
- **Dependency management:** Install only the packages required by that project.
- **Project independence:** Changes to one project's packages are less likely to affect another project.
- **Reproducibility:** Record package versions so the environment can be recreated later.

A virtual environment does not necessarily contain a completely independent copy of the entire Python installation. It commonly references the base Python installation while keeping project packages separate.

**Best practice:** Create a virtual environment for each Python project, especially when working with AI, data science, automation, or application development.

## 4. Understanding Python Packages

A Python package is reusable code created by developers to provide specific functionality.

Instead of writing every feature from scratch, you can install packages and import their functionality into your programs.

Examples include:

| Package | Common use |
|---|---|
| `requests` | Making HTTP requests to web services |
| `pandas` | Data analysis and data manipulation |
| `openai` | Accessing OpenAI APIs |
| `numpy` | Numerical computing |
| `fastapi` | Building APIs and web services |

Different projects may require different versions of these packages. Virtual environments allow you to manage those dependencies separately.

## 5. Create Your First Virtual Environment

Let's create a virtual environment for your existing `python-for-ai` project.

There are two common methods.

### Method 1: Create a Virtual Environment Using VS Code

1. Open your `python-for-ai` project folder in VS Code.
2. Open the Command Palette:
   - Windows/Linux: `Ctrl + Shift + P`
   - macOS: `Cmd + Shift + P`
3. Search for `Python: Create Environment`.
4. Select `Venv`.
5. Select the Python interpreter you installed earlier.
6. If prompted to select a dependency file, choose one if your project already has one; otherwise, skip this step.

VS Code will create a `.venv` directory and configure the project to use the environment.

### Method 2: Create a Virtual Environment Using the Terminal

Open the integrated terminal in VS Code and make sure you are inside your `python-for-ai` project directory.

Run:

**Windows, macOS, or Linux:**

```bash
python -m venv .venv
```

If `python` is not the correct command on your system, use the appropriate alternative.

Windows:

```powershell
py -m venv .venv
```

macOS/Linux:

```bash
python3 -m venv .venv
```

### Understanding the Command

```bash
python -m venv .venv
```

- `python`: Runs the selected Python interpreter.
- `-m`: Tells Python to execute a module.
- `venv`: Python's built-in module for creating virtual environments.
- `.venv`: The directory where the virtual environment will be created.

## 6. Understand the Project Structure

After creating the virtual environment, your project will look similar to this:

```text
python-for-ai/
├── .venv/
├── hello.py
└── python-for-ai.code-workspace
```

The `.venv` directory contains the environment's Python executable or reference, package directories, and activation scripts.

The exact directory structure varies by operating system.

The dot at the beginning of `.venv` makes it a hidden directory by convention on Unix-like systems. On Windows, it is not automatically hidden simply because its name starts with a dot.

You generally do not need to edit the contents of `.venv` manually.

## 7. Activate Your Virtual Environment

Activation configures your terminal so that commands such as `python` and `pip` use the virtual environment by default.

### Windows PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

### Windows Command Prompt

```bat
.venv\Scripts\activate.bat
```

### macOS/Linux

```bash
source .venv/bin/activate
```

After successful activation, your terminal prompt will usually display `(.venv)`.

For example:

```text
(.venv) PS C:\Users\YourName\Documents\PythonProjects\python-for-ai>
```

This indicates that the virtual environment is active in that terminal session.

## 8. Select the Virtual Environment in VS Code

To make sure VS Code uses the correct interpreter:

1. Open the Command Palette.
2. Search for `Python: Select Interpreter`.
3. Choose the interpreter located inside your project's `.venv` directory.
4. Open a new terminal if necessary.
5. Confirm that the selected environment is being used.

Typical interpreter paths include:

**Windows:**

```text
.venv\Scripts\python.exe
```

**macOS/Linux:**

```text
.venv/bin/python
```

VS Code can automatically activate the selected environment in newly created terminals, depending on its configuration.

**Important:** Selecting an interpreter and activating a terminal environment are related but different operations. If necessary, activate the environment manually.

## 9. Verify Your Virtual Environment

Run the following command in your activated terminal:

```bash
python --version
```

Then check which Python executable is being used:

```bash
python -c "import sys; print(sys.executable)"
```

The path should point to the `.venv` directory within your project.

You can also run this Python code:

```python
import sys

print("Python version:", sys.version)
print("Python executable:", sys.executable)
print("Virtual environment:", sys.prefix != sys.base_prefix)
```

The last line should display:

```text
Virtual environment: True
```

This confirms that the program is running inside a virtual environment.

## 10. Install Packages Inside Your Virtual Environment

Once your environment is activated, install packages using `python -m pip`.

For example:

```bash
python -m pip install requests
```

Verify the installation:

```bash
python -c "import requests; print(requests.__version__)"
```

Because the virtual environment is active, the package will normally be installed into that environment rather than the shared base environment.

To list installed packages, run:

```bash
python -m pip list
```

### Save Your Dependencies

You can record your project's installed packages in a requirements file:

```bash
python -m pip freeze > requirements.txt
```

This creates a `requirements.txt` file containing the installed package versions.

Another environment can install those recorded versions using:

```bash
python -m pip install -r requirements.txt
```

For larger projects, remember that `pip freeze` records all installed packages in the environment, including transitive dependencies. More advanced dependency-management approaches may be preferable for complex applications.

## 11. Deactivate Your Virtual Environment

When you finish working, you can deactivate the current environment:

```bash
deactivate
```

This returns your terminal to its previous Python environment.

Deactivation does not delete your virtual environment or uninstall its packages.

You can reactivate it the next time you work on the project.

## 12. Common Virtual Environment Problems

### Problem 1: Python Command Not Found

Try checking the available Python commands:

```powershell
python --version
py --version
```

On macOS/Linux, also try:

```bash
python3 --version
```

Use the command that points to your intended Python installation.

### Problem 2: PowerShell Blocks Activation

If PowerShell reports that script execution is disabled, you can use the environment's interpreter directly:

```powershell
.\.venv\Scripts\python.exe --version
```

Alternatively, use Command Prompt and activate the environment with:

```bat
.venv\Scripts\activate.bat
```

### Problem 3: VS Code Does Not Recognize the Environment

1. Confirm that `.venv` exists in your project directory.
2. Open the Command Palette.
3. Select `Python: Select Interpreter`.
4. Choose the interpreter inside `.venv`.
5. Open a new terminal and verify the executable path.

If the environment is missing or damaged, you may need to recreate it.

### Problem 4: Package Not Found

If you encounter `ModuleNotFoundError`, check that the package is installed in the same environment used to run the program.

Run:

```bash
python -m pip show requests
```

Replace `requests` with the package you need to check.

## 13. What About Anaconda?

Anaconda is a Python distribution that includes tools for managing environments and packages. It is popular in data science and scientific computing.

However, you do not need Anaconda to learn Python or create virtual environments.

For this course, we will use:

- Standard Python 3.
- Visual Studio Code.
- The built-in `venv` module.
- `pip` for package installation.

This setup is lightweight and suitable for learning Python, AI engineering, APIs, and automation.

## 14. Lesson Summary

In this lesson, you learned:

- What a Python environment is.
- Why shared package installations can cause dependency conflicts.
- What virtual environments are and how they help isolate dependencies.
- How to create a `.venv` directory using VS Code or the terminal.
- How to activate and select a virtual environment.
- How to install packages and verify the Python interpreter.
- How to troubleshoot common environment issues.

**Next lesson:** Installing Python Packages and Managing Project Dependencies.
