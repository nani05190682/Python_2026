# Organizing Code in Python
## Split Code into Reusable Functions and Modules

### 1. Why organize your code?

When you start learning Python, writing everything in one file is perfectly fine. But as your application grows, a single file can become difficult to read, debug, test, and maintain.

The solution is to break your code into **functions and modules**.

- **Functions** group related instructions into reusable blocks of code.
- **Modules** are Python files that contain functions, classes, and other reusable code.
- **Packages** organize related modules into directories.

Organizing your code provides several benefits:

| Benefit | Explanation |
|---|---|
| Reusability | Write a function once and use it multiple times. |
| Readability | Make your main program easier to understand. |
| Maintainability | Update a function without searching through a large script. |
| Testability | Test individual functions independently. |
| Collaboration | Allow different developers to work on separate modules. |

In this lesson, we will improve our existing `sales-analysis` project by moving reusable functions into a separate Python file.

### 2. Understand the project structure

Our project currently contains a CSV file and a main Python script.

Let's organize it into the following structure:

```text
sales-analysis/
├── analyzer.py
├── helpers.py
├── data/
│   └── sales.csv
└── output/
```

Each file has a specific responsibility:

- `analyzer.py` — runs the sales analysis workflow.
- `helpers.py` — contains reusable helper functions.
- `data/sales.csv` — stores the original sales data.
- `output/` — stores generated reports.

This separation makes the application easier to understand and extend.

### 3. Create reusable helper functions

Inside the `sales-analysis` folder, create a new file named `helpers.py`.

Add the following code:

```python
# helpers.py

def calculate_total(quantity, price):
    """Calculate the total price for a quantity of items."""
    return quantity * price


def format_currency(amount):
    """Format a number as a currency string."""
    return f"${amount:,.2f}"
```

Let's understand these functions.

**Function 1: `calculate_total()`**

```python
def calculate_total(quantity, price):
    return quantity * price
```

This function accepts two arguments:

- `quantity` — the number of items.
- `price` — the price per item.

It multiplies them and returns the result.

Example:

```python
total = calculate_total(3, 99.99)
print(total)
```

Output:

```text
299.96999999999997
```

This illustrates a common floating-point precision issue. The underlying result is approximately `299.97`, but binary floating-point arithmetic cannot represent every decimal fraction exactly.

For ordinary display, use the currency-formatting function:

```python
print(format_currency(total))
```

Output:

```text
$299.97
```

**Function 2: `format_currency()`**

```python
def format_currency(amount):
    return f"${amount:,.2f}"
```

The format specification `:,.2f` means:

- `,` — use thousands separators.
- `.2` — display two digits after the decimal point.
- `f` — format the value as a fixed-point number.

For example:

```python
print(format_currency(1250))
print(format_currency(1234567.5))
```

Output:

```text
$1,250.00
$1,234,567.50
```

These functions each perform one clear task, making them useful throughout the project.

*Note:* This example formats amounts using a dollar sign. For financial calculations that require exact decimal arithmetic, Python's `decimal.Decimal` is generally preferable to binary floating-point numbers.

### 4. Import functions from another Python file

Now that `helpers.py` contains our reusable functions, we can import them into `analyzer.py`.

Python files can be imported as modules when they are available through Python's module search path.

For our simple project, both files are in the same directory:

```text
sales-analysis/
├── analyzer.py
└── helpers.py
```

Inside `analyzer.py`, write:

```python
from helpers import calculate_total, format_currency
```

This statement means:

- Find the `helpers` module.
- Import `calculate_total`.
- Import `format_currency`.

You can now call both functions directly without writing `helpers.` before their names.

For example:

```python
from helpers import calculate_total, format_currency

total = calculate_total(2, 499.99)

print(format_currency(total))
```

Output:

```text
$999.98
```

**Important:** When you run `analyzer.py` normally, Python can generally find `helpers.py` because it is alongside the main script. If the import fails, check your project structure, selected interpreter, and how you launched the program.

### 5. Update `analyzer.py`

Let's use our helper functions to process the sales dataset.

Replace the contents of `analyzer.py` with this example:

```python
from pathlib import Path

import pandas as pd

from helpers import calculate_total, format_currency


# Locate the project directory
project_dir = Path(__file__).resolve().parent

# Locate the input file
data_path = project_dir / "data" / "sales.csv"

# Read the sales data
df = pd.read_csv(data_path)

# Calculate the total for each sales record
df["total"] = [
    calculate_total(quantity, price)
    for quantity, price in zip(df["quantity"], df["price"])
]

# Display the sales data
print("Sales Data")
print("==========")

for _, row in df.iterrows():
    product = row["product"]
    total = format_currency(row["total"])

    print(f"{product}: {total}")

# Calculate and display the grand total
grand_total = df["total"].sum()

print(f"\nGrand Total: {format_currency(grand_total)}")
```

Run the program from the VS Code terminal:

```bash
python analyzer.py
```

Example output:

```text
Sales Data
==========
Laptop: $1,999.98
Mouse: $149.95
Keyboard: $239.97
Monitor: $299.99
Laptop: $999.99
Mouse: $299.90
Keyboard: $159.98
Monitor: $599.98

Grand Total: $4,749.74
```

**Why use `zip()` here?**

The expression:

```python
zip(df["quantity"], df["price"])
```

pairs each quantity with its corresponding price. The list comprehension passes each pair to `calculate_total()` and collects the returned values.

Pandas can also calculate the entire column directly:

```python
df["total"] = df["quantity"] * df["price"]
```

That vectorized expression is shorter and usually more efficient for this simple calculation. We use the helper function here to demonstrate how reusable functions can be integrated into a workflow.

### 6. Understand how Python imports work

Consider this statement:

```python
from helpers import calculate_total
```

Python searches for the `helpers` module using its import system. When it finds the module, it executes the module's top-level statements and makes the requested function available in the importing module.

For a simple project, the following structure is sufficient:

```text
sales-analysis/
├── analyzer.py
└── helpers.py
```

However, importing a module does not mean that Python automatically finds every `.py` file anywhere on your computer. The module must be discoverable through the import search path.

Python also caches imported modules in `sys.modules` during the current process, so importing the same module again generally does not execute its top-level code a second time.

**Alternative import style**

You can import the entire module:

```python
import helpers

total = helpers.calculate_total(2, 100)
print(helpers.format_currency(total))
```

Output:

```text
$200.00
```

Both approaches are valid. Importing specific functions makes their names directly available, while importing the module keeps the origin of each function explicit.

### 7. Organize the project into multiple modules

As your application grows, you can separate different responsibilities into different files.

For example:

```text
sales-analysis/
├── analyzer.py
├── helpers.py
├── reporting.py
├── data/
│   └── sales.csv
└── output/
```

Each module can have a distinct responsibility.

- `analyzer.py` — coordinates the workflow.
- `helpers.py` — contains reusable calculation and formatting functions.
- `reporting.py` — creates and saves reports.

You could move report-related functions into `reporting.py` and import them into `analyzer.py` when needed.

The main program then becomes a coordinator rather than a file containing every calculation, file operation, and reporting instruction.

### 8. Best practices for organizing Python code

Follow these guidelines as your projects grow:

1. **Give functions one clear responsibility.** A function should ideally do one logical task.
2. **Use descriptive names.** Names such as `calculate_total()` and `format_currency()` explain what the functions do.
3. **Avoid unnecessary duplication.** If the same logic appears in several places, consider making it a reusable function.
4. **Keep imports near the top of the module.** This makes dependencies easier to identify.
5. **Avoid executing large workflows during import.** Put application startup logic inside a `main()` function.
6. **Use clear module names.** Prefer `helpers.py` or `reporting.py` over vague names such as `stuff.py`.
7. **Test functions independently.** Verify calculations and formatting before using them in a larger workflow.
8. **Use a package when the project grows.** Related modules can be organized into a package with a clear structure.

A common pattern is:

```python
def main():
    # Run
