# Python Environment: Interactive Python in VS Code

**Lesson: Interactive Python — Write, Run, and Experiment with Code**

## 1. Introduction to Interactive Python

When learning Python, you usually write code in a `.py` file and run the entire file to see the output.

However, sometimes you want to execute only a few lines, inspect a variable, or test an idea without rerunning the entire program.

This is where **Interactive Python** becomes useful.

VS Code supports interactive execution through its Python and Jupyter extensions. You can write code in a regular Python file, execute selected sections, and inspect the results in an Interactive Window.

This approach is particularly useful when learning Python, exploring data, experimenting with AI models, and developing machine learning applications.

## 2. What Is Interactive Python?

Interactive Python allows you to execute code in small sections and immediately observe the results.

Think of it like cooking and tasting your food as you prepare it instead of waiting until the entire meal is finished.

With interactive execution, you can:

- Write code in a `.py` file.
- Execute selected lines or code cells using `Shift + Enter`.
- View output in the Jupyter Interactive Window.
- Inspect variables and experiment with calculations.
- Reuse variables and objects across executions within the same running kernel.

Unlike a conventional script execution, which normally starts a new process for each run, an interactive session can preserve its execution state between runs.

## 3. Why Is Interactive Python Useful for AI Development?

AI engineering often involves experimentation and repeated testing.

For example, you may need to:

- Inspect data before processing it.
- Test data transformations.
- Experiment with different model parameters.
- Examine API responses.
- Evaluate the output of an AI model.
- Compare alternative implementations.

Running an entire program after every small change can slow down this process.

Interactive execution lets you test individual sections and observe the results immediately.

**Example:** When working with a dataset, you can load the data once, inspect its structure, modify a transformation, and rerun only the relevant section.

## 4. Prerequisites

Before setting up Interactive Python, make sure you have:

- Python 3 installed.
- Visual Studio Code installed.
- The Microsoft Python extension installed.
- The Jupyter extension installed.
- A Python virtual environment created for your project.

For this lesson, we will use the existing `python-for-ai` project.

## 5. Install the Required Package

Interactive execution in VS Code uses Jupyter infrastructure. The `ipykernel` package provides the Python kernel that executes code in the Interactive Window.

### Step 1: Open Your Project

Open the `python-for-ai` folder in VS Code.

### Step 2: Activate Your Virtual Environment

**Windows PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
source .venv/bin/activate
```

Your terminal should indicate that the environment is active, usually by displaying `(.venv)`.

### Step 3: Install ipykernel

Run the following command:

```bash
python -m pip install ipykernel
```

This installs `ipykernel` into the active environment.

### Step 4: Install the VS Code Extensions

Open the Extensions panel in VS Code and install these extensions if they are not already installed:

- **Python** by Microsoft
- **Jupyter** by Microsoft

The Python extension provides Python development support, while the Jupyter extension enables interactive execution and notebook functionality.

## 6. Create Your First Interactive Python File

Create a new file named:

`interactive_demo.py`

Add the following code:

```python
# Section 1: Display a greeting
name = "Python Learner"
print(f"Hello, {name}!")

# Section 2: Create a list
numbers = [1, 2, 3, 4, 5]
print(f"Numbers: {numbers}")

# Section 3: Calculate the total
total = sum(numbers)
print(f"Total: {total}")
```

Save the file.

### Understanding the Code

- `name` stores a string.
- `numbers` stores a list of integers.
- `sum(numbers)` calculates the sum of the list values.
- `total` stores the calculated result.
- `print()` displays the output.
- An `f-string` allows variables and expressions to be inserted into a string.

## 7. Execute Code Using Shift + Enter

Follow these steps:

1. Open `interactive_demo.py`.
2. Place your cursor inside the first section, or select the code you want to execute.
3. Press `Shift + Enter`.
4. If prompted, select your `.venv` Python environment.
5. View the results in the Jupyter Interactive Window.

Depending on your VS Code version and configuration, you may be prompted to create or open an Interactive Window.

### Expected Output

```text
Hello, Python Learner!
Numbers: [1, 2, 3, 4, 5]
Total: 15
```

You can execute individual sections without rerunning unrelated sections of your program.

**Note:** `Shift + Enter` executes the current line, selected code, or current code cell according to the editor context and configuration. If necessary, select the desired lines before using the shortcut.

## 8. Organize Code into Interactive Cells

VS Code supports cell-based interactive execution in Python files using special comments.

A cell begins with `# %%`.

Update your file as follows:

```python
# %% Section 1: Greeting
name = "Python Learner"
print(f"Hello, {name}!")

# %% Section 2: Working with lists
numbers = [1, 2, 3, 4, 5]
print(f"Numbers: {numbers}")

# %% Section 3: Calculations
total = sum(numbers)
print(f"Total: {total}")
```

VS Code recognizes these markers and displays **Run Cell** and **Run Below** actions above the relevant sections.

You can now execute each section independently.

For example:

- Run Cell in Section 1 to display the greeting.
- Run Cell in Section 2 to create and display the list.
- Run Cell in Section 3 to calculate the total.

If Section 3 is executed before Section 2 has defined `numbers` in the current kernel, Python will raise a `NameError`.

This is because interactive execution depends on the current kernel state.

## 9. Understand Variable Persistence

One of the main benefits of interactive execution is that variables remain available in the same running kernel.

Let's explore this behavior.

### Step 1: Create a Variable

Execute this code:

```python
message = "Hello"
```

### Step 2: Reuse the Variable

In another cell,
