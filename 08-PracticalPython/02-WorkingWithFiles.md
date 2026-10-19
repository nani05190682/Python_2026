# Working with Files in Python
## Read, Process, and Write Data Files

### 1. Why do we work with files in AI projects?

When developing Python applications, you will frequently need to read, process, and save data.

In AI engineering, data might come from APIs, databases, spreadsheets, documents, log files, or other systems. Python allows you to work with these files and prepare data for analysis, automation, and AI applications.

Common file formats include:

| Format | Extension | Common use |
|---|---|---|
| CSV | `.csv` | Tabular data from spreadsheets and databases. |
| JSON | `.json` | API responses, configuration, and structured data. |
| Text | `.txt` | Logs, notes, and raw text. |
| XML | `.xml` | Structured data exchanged between systems. |
| Excel | `.xlsx` | Business reports and spreadsheets. |
| Parquet | `.parquet` | Efficient storage for analytical datasets. |
| PDF | `.pdf` | Documents, reports, and reference material. |

Python has built-in modules and third-party libraries for working with these formats.

### 2. Understand the common file-handling libraries

Different file types are best handled by different libraries.

| Library | Purpose |
|---|---|
| `open()` | Built-in function for reading and writing files. |
| `csv` | Built-in module for reading and writing CSV files. |
| `json` | Built-in module for working with JSON data. |
| `pandas` | Reads, processes, analyzes, and writes tabular data. |
| `xml.etree.ElementTree` | Built-in module for parsing XML. |
| `openpyxl` | Reads and writes Excel `.xlsx` workbooks. |
| `pypdf` | Reads and processes PDF documents. |
| `pyarrow` | Supports formats such as Parquet. |

For this lesson, we will primarily use `pandas`, `json`, and Python's built-in file operations.

### 3. Prepare your project

Let's continue with the `sales-analysis` project from the previous lesson.

Your project should look like this:

```text
sales-analysis/
├── analyzer.py
├── data/
│   └── sales.csv
└── output/
```

The `sales.csv` file contains the following data:

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

Install pandas and the libraries needed for the examples:

```bash
python -m pip install pandas openpyxl
```

We install `openpyxl` because pandas uses an Excel engine such as `openpyxl` to write `.xlsx` files.

### 4. Read a CSV file using pandas

A CSV file stores data in rows and columns. Pandas can load the entire dataset into a DataFrame.

```python
import pandas as pd
from pathlib import Path

# Locate the project directory
project_dir = Path(__file__).resolve().parent

# Define the input file
data_path = project_dir / "data" / "sales.csv"

# Read the CSV file
df = pd.read_csv(data_path)

# Display the data
print("Sales Data:")
print(df)

# Display the number of rows and columns
print(f"\nRows: {df.shape[0]}")
print(f"Columns: {df.shape[1]}")
```

Example output:

```text
Sales Data:
         date   product  quantity   price
0  2024-01-01    Laptop         2  999.99
1  2024-01-01     Mouse         5   29.99
2  2024-01-02  Keyboard         3   79.99
3  2024-01-02   Monitor         1  299.99
4  2024-01-03    Laptop         1  999.99
5  2024-01-03     Mouse        10   29.99
6  2024-01-04  Keyboard         2   79.99
7  2024-01-05   Monitor         2  299.99

Rows: 8
Columns: 4
```

**Understanding the code**

- `pd.read_csv()` loads the CSV into a DataFrame.
- `df.shape` returns a tuple containing the number of rows and columns.
- `df.shape[0]` gives the row count.
- `df.shape[1]` gives the column count.

You can also inspect the dataset using:

```python
print(df.head())
print(df.columns)
print(df.dtypes)
```

These statements display the first five rows, column names, and data types.

### 5. Process the data

Reading a file is only the first step. Often, you need to calculate new values or transform the data.

For our sales dataset, revenue is calculated as:

**Revenue = Quantity × Price**

Add this code after loading the CSV:

```python
# Calculate revenue for each sales record
df["total"] = df["quantity"] * df["price"]

print(df)
```

Example output:

```text
         date   product  quantity   price    total
0  2024-01-01    Laptop         2  999.99  1999.98
1  2024-01-01     Mouse         5   29.99   149.95
2  2024-01-02  Keyboard         3   79.99   239.97
3  2024-01-02   Monitor         1  299.99   299.99
4  2024-01-03    Laptop         1  999.99   999.99
5  2024-01-03     Mouse        10   29.99   299.90
6  2024-01-04  Keyboard         2   79.99   159.98
7  2024-01-05   Monitor         2  299.99   599.98
```

The `total` column is calculated in memory. The original CSV file remains unchanged unless you explicitly write the updated DataFrame back to a file.

Calculate the total revenue across all records:

```python
total_revenue = df["total"].sum()

print(f"Total revenue: ${total_revenue:,.2f}")
```

Output:

```text
Total revenue: $4,749.74
```

### 6. Write data to a JSON file

JSON is commonly used for APIs, web applications, and configuration files.

Pandas can convert a DataFrame into JSON.

```python
import json
from pathlib import Path

output_dir = project_dir / "output"
output_dir.mkdir(parents=True, exist_ok=True)

json_path = output_dir / "sales_data.json"

df.to_json(
    json_path,
    orient="records",
    indent=2,
    date_format="iso"
)

print(f"JSON saved to: {json_path}")
```

The resulting JSON contains an array of objects, with each object representing one sales record.

Example:

```json
[
  {
    "date": "2024-01-01",
    "product": "Laptop",
    "quantity": 2,
    "price": 999.99,
    "total": 1999.98
  },
  {
    "date": "2024-01-01",
    "product": "Mouse",
    "quantity": 5,
    "price": 29.99,
    "total": 149.95
  }
]
```

This is an illustrative excerpt; the actual file contains all eight records.

**What does `orient="records"` mean?**

It tells pandas to represent each row as a JSON object and place the objects in a list.

The `indent=2` argument makes the JSON easier for humans to read. `date_format="iso"` formats datetime values using ISO-style date strings.

### 7. Write data to an Excel file

Excel is useful when sharing reports with business users who prefer spreadsheets.

```python
excel_path = output_dir / "sales_data.xlsx"

df.to_excel(excel_path, index=False)

print(f"Excel file saved to: {excel_path}")
```

The file will be saved as `sales_data.xlsx`.

**Why use `index=False`?**

Pandas uses a row index internally. Setting `index=False` prevents that index from being added as an unnecessary column in the exported spreadsheet.

Unlike CSV, an Excel workbook can also contain formatting, formulas, multiple worksheets, and other spreadsheet features.

### 8. Save the processed data to CSV

You can save the DataFrame with the newly calculated revenue column.

```python
csv_output_path = output_dir / "sales_with_totals.csv"

df.to_csv(csv_output_path, index=False)

print(f"Processed CSV saved to: {csv_output_path}")
```

The output CSV now contains five columns:

```csv
date,product,quantity,price,total
2024-01-01,Laptop,2,999.99,1999.98
2024-01-01,Mouse,5,29.99,149.95
```

The example above shows only the first two records.

This is a common data-processing workflow: read an input file, transform its contents, and save the result separately.

### 9. Read a JSON file

Python includes a built-in `json` module for loading and saving JSON data.

Suppose you have a file named `config.json`:

```json
{
  "project": "sales-analysis",
  "environment": "development",
  "debug": true,
  "max_records": 1000
}
```

You can read it like this:

```python
import json
from pathlib import Path

config_path = project_dir / "data" / "config.json"

with open(config_path, "r", encoding="utf-8") as file:
    config = json.load(file)

print(config)
print("Project:", config["project"])
print("Environment:", config["environment"])
print("Debug enabled:", config["debug"])
```

The `json.load()` function reads JSON from an open file and converts it into Python objects. In this example, the top-level JSON object becomes a Python dictionary.

**Remember the difference:**

```python
json.load(file)       # Read JSON from a file object
json.loads(text)      # Parse JSON from a string
json.dump(data, file) # Write JSON to a file object
json.dumps(data)      # Convert Python data into a JSON string
```

### 10. Read a text file

Text files are useful for notes, logs, documents, and raw text that you may later process using Python or an AI model.

Create a file named `notes.txt` inside your `data` folder:

```text
Python is useful for data processing.
APIs connect applications.
AI systems can analyze structured and unstructured data.
```

Read the file:

```python
text_path = project_dir / "data" / "notes.txt"

with open(text_path, "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

The `with` statement automatically closes the file when the block finishes, including when an exception occurs.

Other useful file-reading methods include:

```python
file.read()       # Read the remaining content as one string
file.readline()   # Read one line
file.readlines()  # Read remaining lines into a list
```

For large files, reading line by line is often more memory-efficient than loading the entire file into memory.

```python
with open(text_path, "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

### 11. Write and append to a text file

Python supports several file modes.

| Mode | Meaning |
|---|---|
| `"r"` | Read an existing file. |
| `"w"` | Write to a file, replacing its existing contents. |
| `"a"` | Append to the end of a file. |
| `"x"` | Create a new file and fail if it already exists. |

Create a report using write mode:

```python
report_path = output_dir / "summary.txt"

with open(report_path, "w", encoding="utf-8") as file:
    file.write("Sales Analysis Report\n")
    file.write("=====================\n")
    file.write(f"Number of records: {len(df)}\n")
    file.write(f"Total revenue: ${df['total'].sum():,.2f}\n")

print(f"Report saved to: {report_path}")
```

To append a new line without replacing the existing report:

```python
with open(report_path, "a", encoding="utf-8") as file:
    file.write("Analysis completed successfully.\n")
```

**Important:** Opening an existing file in `"w"` mode truncates its contents. Use `"a"` when you want to append.

### 12. Understand other file formats

You will encounter other file formats as you advance in Python and AI engineering.

**XML**

XML stores structured data using nested tags. Python includes `xml.etree.ElementTree` for parsing XML documents.

**Parquet**

Parquet is a column-oriented format commonly used for analytical datasets. It can be useful when working with larger datasets and data-processing systems.

**PDF**

PDF files often contain reports, manuals, or documents. A library such as `pypdf` can extract text from many PDFs, although scanned documents may require OCR.

**Excel**

Excel files are useful for business reports and spreadsheet workflows. Pandas can read them using `pd.read_excel()` when an appropriate engine is installed.

For example:

```python
# Read an Excel workbook
df = pd.read_excel("data/sales_data.xlsx")

# Read a Parquet dataset
df = pd.read_parquet("data/sales_data.parquet")
```

These examples assume the files exist and the required dependencies are installed. Parquet support typically requires `pyarrow` or another supported engine.

### 13. Complete example: Read, process, and save files

Let's combine the concepts into one program.

This version uses `pathlib` to make file paths reliable, pandas to process the sales dataset, and JSON, CSV, and Excel writers to save the results.

```python
from pathlib import Path
import pandas as pd

# 1. Find the project directory
project_dir = Path(__file__).resolve().parent

# 2. Define the input and output paths
data_path = project_dir / "data" / "sales.csv"
output_dir = project_dir / "output"

# 3. Create the output directory
output_dir.mkdir(parents=True, exist_ok=True)

# 4. Check that the input file exists
if not data_path.exists():
    raise FileNotFoundError(f"Input file not found: {data_path}")

# 5. Load the CSV data
df = pd.read_csv(data_path)

# 6. Calculate revenue for each record
df["total"] = df["quantity"] * df["price"]

# 7. Calculate total revenue
total_revenue = df["total"].sum()

print("Sales Analysis")
print("==============")
print(df.to_string(index=False))
print(f"\nTotal revenue: ${total_revenue:,.2f}")

# 8. Save the processed data in multiple formats
df.to_csv(output_dir / "sales_with_totals.csv", index=False)

df.to_json(
    output_dir / "sales_data.json",
    orient="records",
    indent=2,
    date_format="iso"
)

df.to_excel(output_dir / "sales_data.xlsx", index=False)

# 9. Write a text summary
with open(output_dir / "summary.txt", "w", encoding="utf-8") as file:
    file.write("Sales Analysis Summary\n")
    file.write("======================\n")
    file.write(f"Records processed: {len(df)}\n")
    file.write(f"Total revenue: ${total_revenue:,.2f}\n")

print("\nOutput files created successfully.")
```

Run the program from the VS Code terminal:

```bash
python analyzer.py
```

Your project should now look like this:

```text
sales-analysis/
├── analyzer.py
├── data/
│   └── sales.csv
└── output/
    ├── sales_with_totals.csv
    ├── sales_data.json
    ├── sales_data.xlsx
    └── summary.txt
```

### 14. Best practices for working with files

Follow these practices in your projects:

1. **Use `with open(...)` for file operations.** This ensures files are closed automatically.
2. **Specify an encoding.** For text files, `encoding="utf-8"` is a good default.
3. **Use `pathlib`.** It helps build clear, cross-platform paths.
4. **Check for missing input files.** Provide useful errors instead of confusing failures.
5. **Keep original data separate from processed data.** Save generated files to an output directory.
6. **Be careful with write mode.** `"w"` replaces existing contents.
7. **Validate external data.** Files from APIs or other systems may contain missing fields, unexpected values, or invalid formats.
8. **Avoid loading huge files all at once.** Use chunked reading or streaming when necessary.
9. **Protect sensitive information.** Do not accidentally export passwords, API keys, or confidential records.

### 15. Practice exercises

**Exercise 1: Read a CSV file**

Load `sales.csv` and display the first three rows.

**Exercise 2: Calculate revenue**

Add a `total` column by multiplying `quantity` by `price`.

**Exercise 3: Export to JSON**

Save the processed dataset as `sales.json` in the `output` folder.

**Exercise 4: Create a text summary**

Write the number of sales records and total revenue to `summary.txt`.

**Exercise 5: Read JSON configuration**

Create `config.json` with a project name and environment. Read the file and print the values.

**Exercise 6: Append to a file**

Append the message `Processing completed` to `summary.txt` without deleting the existing summary.

### 16. Lesson summary

In this lesson, you learned how to:

- Read CSV files with pandas.
- Calculate new columns and analyze data.
- Write CSV, JSON, and Excel files.
- Read JSON configuration files.
- Read, write, and append to text files.
- Use Python's built-in `json` module.
- Organize files with `pathlib`.
- Understand common file modes and file-handling best practices.

**Key takeaway:** File handling is a fundamental Python skill. It allows you to bring data into your application, transform it, and save the results for later use.

In AI engineering, these skills are essential for preparing datasets, processing API responses, reading logs, managing configuration, and preparing documents for AI workflows.

**Next lesson: Error Handling in Python — Manage Exceptions and Build Reliable Programs.**
