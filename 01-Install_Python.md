# Lesson 01: Python Installation and Environment Setup

Beginner Level • Hands-on Practice • Windows 10/11 • VS Code

By the end of this lesson, you will be able to install Python, configure Visual Studio Code (VS Code), create a virtual environment, and run your first Python program.

## Learning objectives

- Install Python 3 on Windows.
- Verify the Python installation using PowerShell.
- Install and configure VS Code.
- Install the Python extension.
- Select the correct Python interpreter.
- Create and activate a virtual environment.
- Run a Python script and troubleshoot common errors.

## Step 1: Install Python

[Python logo Icons, Logos, Symbols – Free Download PNG, SVG](https://images.openai.com/static-rsc-4/DmsB8FS-GP7uphH6D36okAKArZlBuv18j7laB7MGQztxtnElBP3iuvRtFFsgJN3_CMjTR795lNP5nkz0C0O5HRM_6vUhOfMDScUzQErc9yfIrgdVyj38VLAdNtbsn3vWhJAUhRcvYx9LUssqXM5zJvcGr4rSiP0dNojMqKdTlnc?purpose=inline)

Download Python 3

1. Open the official website: [Python for Windows](https://www.python.org/downloads/windows/?utm_source=chatgpt.com).
2. Download a current, supported Python 3 release.
3. Run the installer.
4. Enable Add python.exe to PATH if the installer offers this option.
5. Click Install Now and wait for installation to finish.

Important

Enable the option to add Python to PATH when available. This helps you run Python from PowerShell or the Command Prompt without specifying its full installation path.

## Step 2: Verify the Python installation

Open Windows PowerShell or the VS Code terminal.

Run these commands one at a time:

Command 1 — Check the Python version

```
python --version
```

Expected output will look like:

```
Python 3.x.x
```

Command 2 — Check the Python launcher

```
py --version
```

Command 3 — Locate Python

```
python -c "import sys; print(sys.executable)"
```

This displays the Python executable currently being used.

If `python` is not recognized, try `py --version`. If the launcher works, you can use `py` to continue while troubleshooting PATH.

## Step 3: Install Visual Studio Code

[File:Visual Studio Code 1.35 icon.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/bwltRsn8xFpdSRcYQ3DdHauINNG_Ll8uEuWak3gU_Cd8IQKU8JMwJXvDy7WOSMXzw_LreGtysSFaVMfFopIshhFxhhA7optqpzdDNA41Fr3DZ8RT6oELKwe8M8zFoIi4_H68G4UOg124XH5x4eObz-mHD-E9xY_6m_hLlZ275hc?purpose=inline)

Download VS Code

1. Visit [Visual Studio Code downloads](https://code.visualstudio.com/Download?utm_source=chatgpt.com).
2. Download the Windows installer.
3. Run the installer and complete setup.
4. Open Visual Studio Code.

## Step 4: Install the Python extension

[Python: VS Code Update, Why It's So Popular (& Famous Easter Egg) -- Visual Studio Magazine](https://images.openai.com/static-rsc-4/WOjdaKejjxmbB-ZXx8vCPFozUyDJ4UTVqc-cTrJK3ak3_4tsz2JVS5beBrMkG_LX0udduhOgYojeno1OwxP7MW_MMki-i0K2GbkwcJpgOZCjgN9nyigxAlFIiohl776gXYflDThsFO2e2HYXiBWn48BB_Eum7Oi0DbXhkNwzVZA?purpose=inline)

[visualstudiomagazine.com](https://visualstudiomagazine.com/articles/2023/03/03/python.aspx?utm_source=chatgpt.com)

1. Open VS Code.
2. Click the Extensions icon in the left sidebar.
3. Search for `Python`.
4. Install Python by Microsoft.

You can also open the official extension page: [Python extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-python.python\&utm_source=chatgpt.com).

The extension provides Python interpreter selection, debugging, code completion, and other development features.

## Step 5: Create your first Python project

Open PowerShell and run:

```
mkdir PythonProjects
cd PythonProjects
mkdir Lesson01
cd Lesson01
code .
```

This creates your project directory and opens it in VS Code. If `code` is not recognized, open VS Code manually and select File → Open Folder.

Your folder structure will be:

```
PythonProjects/
└── Lesson01/
```

In VS Code, create a new file named `hello.py`.

Add this code:

```
print("Hello, World!")print("Welcome to Python programming!")
```

Save the file.

## Step 6: Run your first Python program

Open the VS Code terminal using Terminal → New Terminal.

Run:

```
python hello.py
```

Expected output:

```
Hello, World!
Welcome to Python programming!
```

Congratulations! You have successfully created and run a Python script.

## Step 7: Create a Python virtual environment

A virtual environment keeps project-specific Python packages separate from other projects.

In the VS Code terminal, run:

```
python -m venv .venv
```

This creates a `.venv` directory inside your project.

Activate it in PowerShell:

```
.\.venv\Scripts\Activate.ps1
```

Your terminal prompt should now begin with `(.venv)`.

Verify the environment:

```
python --version
python -c "import sys; print(sys.executable)"
```

The executable path should point to your project's `.venv` directory.

If PowerShell blocks activation because of the execution policy, you can use the environment's Python directly:

```
.\.venv\Scripts\python.exe --version
```

Alternatively, use Command Prompt and activate it with:

```
.venv\Scripts\activate.bat
```

## Step 8: Select the Python interpreter in VS Code

[How to install Python packages for a VS Code virtual environment? - Stack Overflow](https://images.openai.com/static-rsc-4/YwhgGwxkIP8nh0Ozuk_1YK9ip16MnwYr6gbZRnZJMXXufjPsdpu_Fv1i_pjHixNqqhr7tCVo0p13rebXzEa5By3gynt6Q1i7HcYCdGm3gNiiKdSMXUMdww0eB1jv47XMEOoqzsDidpJaC7vL8Yp5r7r73NHp4b_1AAMm4GQ5fJA?purpose=inline)

[stackoverflow.com](https://stackoverflow.com/questions/75935576/how-to-install-python-packages-for-a-vs-code-virtual-environment?utm_source=chatgpt.com)

1. Press `Ctrl + Shift + P`.
2. Search for `Python: Select Interpreter`.
3. Select the interpreter inside your project's `.venv` directory.
4. Open a new terminal if necessary.
5. Run `hello.py` again.

This ensures that VS Code uses the correct Python environment for your project.

## Step 9: Install and test a Python package

With your virtual environment activated, run:

```
python -m pip install requests
```

Using `python -m pip` is generally more reliable than running `pip` directly because it associates package installation with the selected Python interpreter.

Test the installation:

```
python -c "import requests; print(requests.__version__)"
```

If a version number appears, the package is installed successfully.

## Step 10: Understand your final project structure

```
PythonProjects/
└── Lesson01/
    ├── .venv/
    └── hello.py
```

The `.venv` folder contains your isolated environment. It is normally excluded from Git repositories; recreate it from a dependency file when setting up the project on another machine.

## Hands-on practice checklist

### Lesson completion

0 of 8

Install Python 3

Download and install Python from the official website.

Verify Python

Run python --version or py --version.

Install VS Code

Install the editor and Microsoft Python extension.

Create a project

Create Lesson01 and add hello.py.

Run a Python script

Display Hello, World! in the terminal.

Create a virtual environment

Create and activate .venv.

Select the interpreter

Choose the .venv interpreter in VS Code.

Install a package

Install requests using python -m pip.

Reset checklistCopy checklist to GitHub

## Common errors and solutions

| Error                                     | Solution                                                                   |
| ----------------------------------------- | -------------------------------------------------------------------------- |
| `python is not recognized`                | Try `py --version`; check installation and PATH.                           |
| `pip is not recognized`                   | Use `python -m pip install package_name`.                                  |
| VS Code uses the wrong Python             | Run `Python: Select Interpreter`.                                          |
| Virtual environment activation is blocked | Use `.\.venv\Scripts\python.exe` directly or activate from Command Prompt. |
| `ModuleNotFoundError`                     | Install the package in the same environment used to run the script.        |

