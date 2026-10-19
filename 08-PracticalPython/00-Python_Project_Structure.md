# Project Structure in Python
## Organize Your Python Projects

### 1. Why do we need a project structure?

So far, you have written Python programs in individual files. This is a good way to learn Python, but real-world applications usually contain multiple Python files, data files, configuration files, and generated outputs.

As a project grows, keeping everything in one folder becomes difficult to manage.

A good project structure helps you:

- Organize code, data, and output files.
- Find files quickly.
- Reuse code across multiple Python scripts.
- Test and maintain your application more easily.
- Collaborate with other developers.
- Prepare your projects for AI engineering and production environments.

For example, a data analysis application might contain one Python file to load data, another to analyze it, and another to generate reports.

### 2. Organize your existing workspace

You already have a `python-for-ai` workspace from the beginning of this course.

Open that workspace in Visual Studio Code (VS Code). Create a new folder named `sales-analysis`.

Your directory structure should look like this:

```text
python-for-ai/
├── hello.py
└── sales-analysis/
    ├── data/
    └── output/
```

The folders have different purposes:

| Folder or file | Purpose |
|---|---|
| `hello.py` | Your existing Python practice file. |
| `sales-analysis/` | Contains the sales analysis project. |
| `data/` | Stores input datasets such as CSV files. |
| `output/` | Stores generated reports, charts, and results. |

**How to create folders in VS Code**

1. Open the Explorer panel.
2. Right-click the `python-for-ai` folder.
3. Select **New Folder** and enter `sales-analysis`.
4. Right-click `sales-analysis` and create `data`.
5. Repeat the process to create `output`.

Keep your practice files separate from your new project.

### 3. Create a sample data file

Inside `sales-analysis/data/`, create a file named `sales.csv`.

Copy the following content into the file:

```csv
date,product,quantity,price
2024-01-01,Laptop,2,999.99
2024-01-01,Mouse,5,29.99
2024-01-02,Keyboard,3,79.99
2024-01-02,Monitor,1,299.99
2024-01-03,Laptop,1,999.99
2024-01-03,Mouse,10,29.99
2024-01-04,Keyboard,2,79.99
2024-01-05,Monitor,2,299.99
```

Save the file.

Your project now looks like this:

```text
python-for-ai/
├── hello.py
└── sales-analysis/
    ├── data/
    │   └── sales.csv
    └── output/
```

**What is a CSV file?**

CSV stands for Comma-Separated Values. It stores tabular data in plain text, with each line representing a row and commas separating the values.

In our example:

- `date` represents the sale date.
- `product` identifies the product sold.
- `quantity` represents the number of units sold.
- `price` represents the price per unit.

We will use this dataset in later exercises to calculate revenue and analyze sales trends.

### 4. Understand file paths

A file path tells Python where a file is located.

Consider this project structure:

```text
sales-analysis/
├── analyzer.py
├── data/
│   └── sales.csv
└── output/
```

If `analyzer.py` is run with `sales-analysis` as its current working directory, these relative paths point to the expected locations:

```python
"data/sales.csv"
"output/report.json"
```

The first path identifies the input dataset. The second identifies a location where a report could be saved.

**What is a relative path?**

A relative path identifies a file or folder in relation to another directory, usually the current working directory when using ordinary relative file paths.

For example:

```python
import os

print(os.getcwd())
```

`os.getcwd()` displays the current working directory.

You might see output similar to:

```text
/Users/student/python-for-ai/sales-analysis
```

The actual path depends on your computer and how you launch Python.

**Important:** The directory containing your Python script and the current working directory are not necessarily the same. VS Code's Run button, an integrated terminal, and an interactive window can use different working directories.

We will make our file paths more reliable in a later step.

### 5. Create your first project script

Inside the `sales-analysis` folder, create a Python file named `analyzer.py`.

Add the following code:

```python
import os

# Display the current working directory
print("Current directory:", os.getcwd())

# Define the relative path to the CSV file
data_path = "data/sales.csv"

# Check whether the file exists
if os.path.exists(data_path):
    print(f"Found {data_path}")
else:
    print(f"Cannot find {data_path}")
    print("Check your current working directory.")
```

Save the file.

**Understanding the code**

- `import os` imports Python's built-in operating-system utilities.
- `os.getcwd()` displays the current working directory.
- `data_path` stores the path to the CSV file.
- `os.path.exists()` checks whether the specified path exists.
- `if` and `else` select the appropriate message.

If the path is correct, the output will look similar to:

```text
Current directory: /Users/student/python-for-ai/sales-analysis
Found data/sales.csv
```

If the file cannot be found, check that you created it in the correct folder and that Python is running with the expected working directory.

### 6. Run your program in VS Code

There are two common ways to run your script.

#### Option 1: Use the Run button

1. Open `analyzer.py`.
2. Ensure the correct Python interpreter is selected.
3. Click the **Run Python File** play button in the top-right corner.
4. Check the output in the integrated terminal.

This runs the Python file as a script.

#### Option 2: Use the integrated terminal

Open the VS Code terminal and navigate to the project folder:

```bash
cd sales-analysis
```

Run the script:

```bash
python analyzer.py
```

On some Linux or macOS systems, use:

```bash
python3 analyzer.py
```

This approach makes the working directory explicit and is useful when learning file paths.

**What about Shift+Enter?**

In VS Code, `Shift+Enter` can send selected code or the current line to an interactive window or Python REPL, depending on the installed extensions and configuration. It is useful for experimenting with individual statements, but it does not necessarily run the entire script with the same working directory as the Run button or terminal.

For this project, use the integrated terminal when you want to run the complete program consistently.

### 7. Make file paths more reliable

Relative paths are convenient, but they can break when a script is launched from a different directory.

Python's `pathlib` module provides a cleaner way to work with paths.

Replace the code in `analyzer.py` with:

```python
from pathlib import Path

# Locate the directory containing this script
project_dir = Path(__file__).resolve().parent

# Build the input and output paths
data_path = project_dir / "data" / "sales.csv"
output_dir = project_dir / "output"

# Check whether the input file exists
if data_path.exists():
    print(f"Found: {data_path}")
else:
    print(f"Cannot find: {data_path}")

# Create the output folder if it does not exist
output_dir.mkdir(parents=True, exist_ok=True)

print(f"Output directory: {output_dir}")
```

**Why is this approach better?**

- `__file__` identifies the Python script's file path when running a normal script.
- `Path(__file__).resolve().parent` identifies the directory containing `analyzer.py`.
- The `/` operator joins path components.
- `exists()` checks whether a path exists.
- `mkdir()` creates the output directory.
- `parents=True` allows missing parent directories to be created.
- `exist_ok=True` prevents an error if the directory already exists.

Now the paths are based on the script's location rather than the terminal's current directory.

This is generally more reliable for small projects and is a useful habit to develop early.

### 8. Read the CSV file with pandas

Let's extend the project by loading the sales dataset.

First, install pandas if it is not already installed:

```bash
python -m pip install pandas
```

Then update `analyzer.py`:

```python
from pathlib import Path
import pandas as pd

# Find the project directory
project_dir = Path(__file__).resolve().parent

# Define the data and output paths
data_path = project_dir / "data" / "sales.csv"
output_dir = project_dir / "output"

# Create the output directory
output_dir.mkdir(parents=True, exist_ok=True)

# Check the input file
if not data_path.exists():
    raise FileNotFoundError(f"Sales file not found: {data_path}")

# Load the CSV file
df = pd.read_csv(data_path)

# Display the dataset
print("Sales Data")
print(df)

# Calculate revenue for each row
df["revenue"] = df["quantity"] * df["price"]

# Calculate total revenue
total_revenue = df["revenue"].sum()

print(f"\nTotal revenue: ${total_revenue:,.2f}")

# Save the processed data
output_path = output_dir / "sales_report.csv"
df.to_csv(output_path, index=False)

print(f"Report saved to: {output_path}")
```

Run the program:

```bash
python analyzer.py
```

The program loads the input file, calculates revenue for each sales row, and saves the processed dataset.

For the sample data, the total revenue is **$3,439.73**.

Your directory structure will now contain the generated report:

```text
sales-analysis/
├── analyzer.py
├── data/
│   └── sales.csv
└── output/
    └── sales_report.csv
```

Notice that the original CSV remains unchanged. The processed data is saved separately in `output/`.

### 9. Best practices for organizing Python projects

As your projects grow, follow these guidelines:

1. **Separate code and data.** Keep Python scripts separate from CSV files and other datasets.
2. **Use descriptive names.** Names such as `analyzer.py`, `sales.csv`, and `sales_report.csv` are easier to understand than `file1.py`.
3. **Keep generated files in an output folder.** This makes results easy to locate.
4. **Use `pathlib` for paths.** It reduces problems caused by different operating systems and working directories.
5. **Use a virtual environment.** Install project dependencies in an isolated environment.
6. **Keep secrets out of source code.** Use environment variables or a secrets manager for credentials.
7. **Use Git for version control.** Track source code and configuration while avoiding unnecessary generated files and sensitive data.
8. **Add a README.** Explain what the project does and how to install and run it.

A later version of this project might look like:

```text
sales-analysis/
├── .venv/
├── data/
│   └── sales.csv
├── output/
│   └── sales_report.csv
├── analyzer.py
├── requirements.txt
├── .gitignore
└── README.md
```

Here, `requirements.txt` lists the Python packages required by the project, `.gitignore` specifies files Git should ignore, and `README.md` documents the project.

### 10. Practice exercises

**Exercise 1: Verify the folder structure**

Print the paths of `sales.csv` and the `output` directory.

**Exercise 2: Handle a missing file**

Temporarily rename `sales.csv` and observe the error. Restore the original filename afterward.

**Exercise 3: Calculate product revenue**

Calculate revenue for each product using:

```python
df["revenue"] = df["quantity"] * df["price"]
```

**Exercise 4: Save a summary**

Save the total revenue in a text file named `summary.txt` inside the `output` directory.

**Exercise 5: Add another data file**

Create a second CSV file inside `data/` and load it using `pathlib`.

### 11. Lesson summary

In this lesson, you learned how to:

- Organize a Python project into folders and files.
- Separate input data from generated output.
- Understand relative paths and working directories.
- Check whether files exist.
- Use `pathlib` to construct reliable paths.
- Load and process CSV data using pandas.
- Save processed results into a dedicated output directory.
- Apply project organization best practices.

**Key takeaway:** Good project structure makes Python applications easier to understand, maintain, test, and extend. Start with a simple structure and introduce additional modules and packages when the project grows.

**Next lesson: Refactoring Your Code — Functions, Modules, and Reusable Components.**
