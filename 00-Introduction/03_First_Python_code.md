# Code Editor: Creating and Running Your First Python Program

**Lesson 02: First Python File**

Learn how to create a Python file, write your first program, select the Python interpreter, and execute code using Visual Studio Code (VS Code).

## 1. Create a New Python File

Before writing Python code, make sure your `python-for-ai` project folder is open in VS Code.

Follow these steps:

1. Open the **Explorer** panel on the left side of VS Code.
2. Click the **New File** icon next to your project folder.
3. Enter the filename `hello.py`.
4. Press **Enter** to create the file.

Make sure you include the `.py` extension. This identifies the file as a Python source file.

Your project structure should now look like this:

```text
python-for-ai/
└── hello.py
```

## 2. Understand File Extensions

A file extension identifies the type of file and helps applications determine how to handle it.

Here are some common file extensions:

| Extension | File type | Purpose |
|---|---|---|
| `.txt` | Text file | Stores plain text |
| `.md` | Markdown file | Stores documentation with formatting |
| `.py` | Python file | Contains Python source code |
| `.json` | JSON file | Stores structured data |
| `.yaml` | YAML file | Stores configuration data |

### What Happens When You Create a `.py` File?

When you open a Python file in VS Code and have the Python extension installed, VS Code can provide:

- Syntax highlighting to make code easier to read.
- Python-specific code completion and suggestions.
- Error checking and debugging support.
- Integration with the selected Python interpreter.
- Commands for running Python programs.

## 3. Write Your First Python Program

Open `hello.py` and type the following code:

```python
print("Hello, World!")
print("I'm learning Python for AI")
```

Save the file using `Ctrl + S` on Windows/Linux or `Cmd + S` on macOS.

### Understand the Code

**What is `print()`?**

The `print()` function displays text, numbers, and other values in the output.

For example:

```python
print("Welcome to Python")
print(100)
print(10 + 20)
```

Output:

```text
Welcome to Python
100
30
```

Each `print()` call normally displays its output on a separate line.

### Understanding Syntax Highlighting

VS Code uses different colors to help you distinguish parts of your code.

For example:

- `print` is recognized as a function.
- Text inside quotation marks is recognized as a string.
- Numbers may have a different color from text.
- Comments are typically displayed in a separate color.

Syntax highlighting improves readability, although it does not guarantee that your code is error-free.

## 4. Select the Python Interpreter

Before running your program, make sure VS Code is using the correct Python interpreter.

Follow these steps:

1. Press `Ctrl + Shift + P` on Windows/Linux or `Cmd + Shift + P` on macOS.
2. Search for `Python: Select Interpreter`.
3. Select the Python 3 installation you want to use.
4. If you have already created a virtual environment, select the interpreter inside `.venv`.

For this lesson, you can use your main Python installation. Later, you will learn why virtual environments are recommended for individual projects.

**Important:** The Python interpreter is not always displayed in the bottom-right corner. Its location depends on your VS Code layout and installed extensions. Use the Command Palette if you cannot find it.

## 5. Run Your Python Program

There are three convenient ways to execute your Python code in VS Code.

### Method 1: Run Python File

1. Open `hello.py`.
2. Click the **Run Python File** button, usually displayed as a play icon in the editor's top-right corner.
3. Select **Run Python File in Terminal** if you are shown a menu.

### Method 2: Use the Right-Click Menu

1. Open `hello.py`.
2. Right-click inside the editor.
3. Select **Run Python File in Terminal**.

### Method 3: Use the Integrated Terminal

Open the VS Code terminal using **Terminal → New Terminal**.

Run:

```powershell
python hello.py
```

On systems where Python is available through `python3`, use:

```bash
python3 hello.py
```

On Windows, you can also use the Python launcher:

```powershell
py hello.py
```

The appropriate command depends on how Python was installed and configured.

## 6. Understand the Program Output

When you run your program, the terminal should display output similar to this:

```text
Hello, World!
I'm learning Python for AI
```

VS Code may also display the command used to launch Python and the path to your file. Those command details can vary by operating system and configuration.

### What Happens When You Run the Program?

1. VS Code invokes the selected Python interpreter.
2. Python opens and processes `hello.py`.
3. Python executes the statements in the program.
4. The `print()` calls display their output in the terminal.

You do not need to understand every part of the command at this stage. Focus on writing the code and checking the output.

## 7. Understand How Python Executes Code

Python normally executes statements sequentially, starting from the first statement and proceeding to the next, unless the program's control flow changes.

Consider this example:

```python
print("Step 1: Start learning Python")
print("Step 2: Write a program")
print("Step 3: Run the program")
```

Output:

```text
Step 1: Start learning Python
Step 2: Write a program
Step 3: Run the program
```

The statements execute in the order in which they appear.

Within an expression, Python follows its language rules for evaluating operators and expressions; execution is not simply left to right in every case.

Later, you will learn how conditional statements, loops, functions, and exceptions affect program execution.

## 8. Run Python Programs Manually from the Terminal

You can execute Python files without using the VS Code Run button.

### Run a File from Its Project Directory

First, navigate to the directory containing `hello.py`.

```powershell
cd "$HOME\Documents\PythonProjects\python-for-ai"
python hello.py
```

Adjust the directory if you created your project elsewhere.

### Run a File Using Its Full Path

You can also run a Python file by providing its full path.

Windows example:

```powershell
python "$HOME\Documents\PythonProjects\python-for-ai\hello.py"
```

macOS/Linux example:

```bash
python3 "$HOME/PythonProjects/python-for-ai/hello.py"
```

These commands work when the specified interpreter is installed and the file exists at the given path.

The Run button in VS Code is a convenient way to launch your program. The underlying process still involves invoking a Python interpreter to execute the file.

## 9. Understand `python`, `python3`, and `py`

Different operating systems and installations may use different commands to launch Python.

| Command | Common usage |
|---|---|
| `python` | Runs the Python interpreter associated with this command |
| `python3` | Commonly used to launch Python 3 on macOS/Linux |
| `py` | Windows Python launcher, when installed |

For example:

```bash
python3 hello.py
```

On Windows:

```powershell
py hello.py
```

**Important:** These commands are not guaranteed to point to the same installation. If you use a virtual environment, activate it first or invoke its interpreter explicitly.

To verify the active interpreter, run:

```python
import sys

print(sys.version)
print(sys.executable)
```

Save the code as `check_python.py` and run it. The output shows the Python version and the path of the interpreter executing the script.

## 10. Work with the Integrated Terminal

The integrated terminal allows you to run commands inside VS Code without opening a separate terminal application.

### Open the Terminal

- Windows/Linux: Press `` Ctrl + ` ``.
- macOS: Press `` Cmd + ` ``.
- Alternatively, select **Terminal → New Terminal**.

The backtick key (`) is usually located near the top-left corner of a keyboard.

### Create a New Terminal

Select **Terminal → New Terminal** or click the plus (`+`) icon in the terminal panel.

### Run Basic Commands

Check the Python version:

```powershell
python --version
```

Clear the terminal:

```powershell
cls
```

On macOS/Linux, use:

```bash
clear
```

You can also use the up-arrow key to recall previously executed commands.

The integrated terminal is useful for running scripts, installing packages, creating virtual environments, and troubleshooting Python programs.

## 11. Experiment with Your Program

Now modify `hello.py` to include a few more messages.

```python
print("Hello, World!")
print("I'm learning Python for AI")
print("My name is Vaithee")
print("Today is a great day to code!")
```

Replace `Vaithee` with your own name if you wish.

Run the program again.

Expected output:

```text
Hello, World!
I'm learning Python for AI
My name is Vaithee
Today is a great day to code!
```

### Practice Exercise

Try these changes:

1. Display your name.
2. Display your age.
3. Display the name of your course.
4. Display a message explaining why you want to learn Python.
5. Add two more `print()` statements of your own.

Observe how the output changes each time you modify and run your program.

## 12. Save Your Work

Save your Python file regularly.

- **Windows/Linux:** `Ctrl + S`
- **macOS:** `Cmd + S`
- Alternatively, select **File → Save**.

VS Code may display a dot on the editor tab when a file has unsaved changes.

## 13. Troubleshooting Common Errors

| Error or issue | What to do |
|---|---|
| `python is not recognized` | Check your Python installation and PATH, or try `py --version` on Windows. |
| `python3: command not found` | Verify Python installation or try the command available on your system. |
| `No such file or directory` | Confirm that you are in the correct project directory and that `hello.py` exists. |
| `ModuleNotFoundError` | Install the required package into the interpreter or virtual environment used by the program. |
| No output appears | Save the file, confirm the code contains `print()` statements, and check the terminal for errors. |
| Wrong interpreter selected | Use `Python: Select Interpreter` in the Command Palette. |

## 14. What You Have Learned

Congratulations! You have completed your first hands-on Python programming exercise.

You have learned how to:

- Create a Python file in VS Code.
- Understand common file extensions.
- Write a simple Python program.
- Use the `print()` function.
- Select a Python interpreter.
- Execute Python code using VS Code and the terminal.
- Understand basic program execution order.
- Save and modify your code.
- Troubleshoot common Python execution problems.




### LAB Exercises

# Lab Exercise 01: Create and Run Your First Python Program

**Course:** Python for AI Engineering
**Topic:** Code Editor, Python Files, and Basic Output
**Difficulty:** Beginner
**Duration:** 20–30 minutes

## 1. Lab Objective

By the end of this lab, students will be able to:

- Create a Python project and a `.py` file in Visual Studio Code.
- Write a simple Python program using the `print()` function.
- Run Python code using the VS Code terminal.
- Understand strings, comments, and program execution order.
- Modify a program and verify its output.

## 2. Prerequisites

Before starting this exercise, ensure that you have:

- Python 3 installed on your computer.
- Visual Studio Code installed.
- The Microsoft Python extension installed in VS Code.
- A project folder named `python-for-ai`.

## 3. Lab Scenario

You are starting your journey as a Python developer. Your first task is to create a program that displays a welcome message, introduces you, and explains your learning goal.

## 4. Step 1: Create a Python File

Open your `python-for-ai` project folder in VS Code.

Create a new file named:

`hello.py`

Your project structure should look like this:

```text
python-for-ai/
└── hello.py
```

## 5. Step 2: Write Your First Python Program

Enter the following code in `hello.py`:

```python
# My first Python program

print("Hello, World!")
print("Welcome to Python programming!")
print("My name is Vaithee.")
print("I am learning Python for AI.")
```

Replace `Vaithee` with your own name.

Save the file using `Ctrl + S` on Windows/Linux or `Cmd + S` on macOS.

## 6. Step 3: Run the Program

Open the VS Code terminal by selecting **Terminal → New Terminal**.

Execute the following command:

```bash
python hello.py
```

If your system uses `python3`, execute:

```bash
python3 hello.py
```

On Windows, you can also use:

```powershell
py hello.py
```

## 7. Step 4: Verify the Output

Your program should display the following output:

```text
Hello, World!
Welcome to Python programming!
My name is Vaithee.
I am learning Python for AI.
```

If your output matches the expected result, your first Python program is working correctly.

## 8. Step 5: Understand the Code

Let's examine the important parts of the program.

| Code                                      | Explanation                                                                   |
| ----------------------------------------- | ----------------------------------------------------------------------------- |
| `# My first Python program`               | A comment that describes the code. Python does not execute it as a statement. |
| `print()`                                 | A built-in function that displays output.                                     |
| `"Hello, World!"`                         | A string containing text.                                                     |
| `print("Welcome to Python programming!")` | Displays a welcome message.                                                   |

### Key Concept: Execution Order

Python executes these statements sequentially, from top to bottom.

For example:

```python
print("Step 1")
print("Step 2")
print("Step 3")
```

Output:

```text
Step 1
Step 2
Step 3
```

The order of the statements determines the order of the output.

## 9. Step 6: Modify the Program

Now add three more `print()` statements to your existing program.

```python
# My Python learning profile

print("Hello, World!")
print("My name is Vaithee.")
print("I am learning Python for AI.")
print("My goal is to become an AI Engineer.")
print("I enjoy learning new technologies.")
print("Today is my first Python lab.")
```

Run the program again.

**Expected output:**

```text
Hello, World!
My name is Vaithee.
I am learning Python for AI.
My goal is to become an AI Engineer.
I enjoy learning new technologies.
Today is my first Python lab.
```

Notice that you can change the displayed text simply by editing the strings inside the quotation marks.

## 10. Practice Exercises

Complete these tasks independently.

### Exercise 1: Personal Introduction

Write a program that displays:

- Your full name.
- Your age.
- Your city.
- Your current profession.
- Your reason for learning Python.

### Exercise 2: Technology Profile

Write a program that displays the following information:

```text
My Technical Profile
--------------------
Operating System: Linux
Cloud Platform: Azure
Programming Language: Python
Goal: Learn AI Automation
```

Use separate `print()` statements for each line.

### Exercise 3: Identify the Error

Examine this code:

```python
print("Welcome to Python)
print("Let's start coding!")
```

Identify the syntax errors and correct the program so that both messages are displayed successfully.

**Hint:** Check the quotation marks in both statements.

## 11. Challenge Exercise

Create a program called `my_learning_goals.py` that displays your personal learning roadmap.

Your output should look similar to this:

```text
================================
       MY LEARNING ROADMAP
================================
1. Learn Python fundamentals
2. Practice programming daily
3. Learn APIs and automation
4. Explore AI and machine learning
5. Build real-world projects
================================
My journey starts today!
```

Use `print()` statements to reproduce the output. You may customize the goals to match your interests.
