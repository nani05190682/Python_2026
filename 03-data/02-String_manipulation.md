# String Manipulation in Python
## Advanced Text Operations

### 1. Introduction to String Manipulation

String manipulation means modifying, combining, searching, and formatting text using Python.

In real-world applications, we often need to:
- Combine a user's first and last name.
- Convert text to uppercase or lowercase.
- Remove unnecessary spaces from user input.
- Search for keywords in log files.
- Replace text in messages or configuration files.
- Format information into readable output.

Python provides built-in string operations and methods that make these tasks easier.

### 2. Combining Strings

There are several ways to combine strings in Python.

#### A. Concatenation using `+`

The `+` operator joins two or more strings.

```python
first_name = "Jane"
last_name = "Doe"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
Jane Doe
```

The `" "` adds a space between the two names.

#### B. Using f-strings

F-strings are a convenient, modern way to combine text with variables. Add the letter `f` before the opening quotation mark and place variables inside curly braces (`{}`).

```python
first_name = "Jane"
age = 25

greeting = f"Hello, {first_name}!"
intro = f"I'm {first_name} and I'm {age} years old."

print(greeting)
print(intro)
```

Output:

```text
Hello, Jane!
I'm Jane and I'm 25 years old.
```

You can also perform calculations inside an f-string.

```python
price = 100
quantity = 3

print(f"Total price: {price * quantity}")
```

Output:

```text
Total price: 300
```

**Tip:** Prefer f-strings when combining variables and text because they are generally easier to read than long concatenation expressions.

### 3. Repeating Strings

The multiplication operator (`*`) repeats a string a specified number of times.

```python
star = "*"
stars = star * 10

print(stars)
```

Output:

```text
**********
```

You can also create separators for reports and console output.

```python
separator = "-" * 20

print(separator)
print("SYSTEM STATUS")
print(separator)
```

Output:

```text
--------------------
SYSTEM STATUS
--------------------
```

Repeating a string zero times produces an empty string.

```python
print("Hello " * 0)
```

Output:

```text

```

### 4. Changing String Case

Python provides built-in string methods for changing the capitalization of text.

| Method | Purpose | Example | Result |
|---|---|---|---|
| `lower()` | Converts text to lowercase | `"Python".lower()` | `"python"` |
| `upper()` | Converts text to uppercase | `"Python".upper()` | `"PYTHON"` |
| `title()` | Capitalizes the beginning of words | `"python programming".title()` | `"Python Programming"` |
| `capitalize()` | Capitalizes the first character and lowercases the rest | `"pYTHON".capitalize()` | `"Python"` |
| `swapcase()` | Reverses the case of letters | `"PyThOn".swapcase()` | `"pYtHoN"` |

Example:

```python
text = "Python Programming"

print(text.lower())
print(text.upper())
print(text.title())
print(text.capitalize())
print(text.swapcase())
```

Output:

```text
python programming
PYTHON PROGRAMMING
Python Programming
Python programming
pYTHON pROGRAMMING
```

These methods are useful when standardizing text before displaying it or comparing user input.

For example:

```python
username = input("Enter your username: ")

username = username.strip().lower()

print(f"Normalized username: {username}")
```

If the user enters `  Vaithee82  `, the output is:

```text
Normalized username: vaithee82
```

Note that converting a username to lowercase is appropriate only if the application's username rules are case-insensitive.

### 5. Cleaning Strings

User input and data from files often contain unnecessary whitespace. Python provides methods to remove it.

#### A. The `strip()` method

`strip()` removes whitespace from both ends of a string.

```python
messy = "   hello world   "

cleaned = messy.strip()

print(cleaned)
```

Output:

```text
hello world
```

#### B. The `lstrip()` method

`lstrip()` removes whitespace from the beginning of a string.

```python
text = "   Python   "

print(text.lstrip())
```

Output:

```text
Python   
```

#### C. The `rstrip()` method

`rstrip()` removes whitespace from the end of a string.

```python
text = "   Python   "

print(text.rstrip())
```

Output:

```text
   Python
```

#### D. Removing specific characters

You can pass a string of characters to `strip()`, `lstrip()`, or `rstrip()`.

```python
price = "$19.99"

print(price.strip("$"))
```

Output:

```text
19.99
```

**Important:** The argument to `strip()` is a set of characters to remove from the ends, not an exact substring to remove.

For example:

```python
text = "xyPythonxy"

print(text.strip("xy"))
```

Output:

```text
Python
```

### 6. Searching Within Strings

Python provides methods to check whether text exists and to find where it occurs.

Let's use this example:

```python
message = "I love Python programming with Python"
```

#### A. Checking whether text exists using `in`

The `in` operator returns `True` if the specified substring is present.

```python
message = "I love Python programming with Python"

print("Python" in message)
print("Java" in message)
```

Output:

```text
True
False
```

#### B. Checking the beginning using `startswith()`

```python
message = "I love Python programming"

print(message.startswith("I"))
print(message.startswith("Python"))
```

Output:

```text
True
False
```

#### C. Checking the ending using `endswith()`

```python
filename = "report.txt"

print(filename.endswith(".txt"))
print(filename.endswith(".pdf"))
```

Output:

```text
True
False
```

This is useful when checking file extensions or identifying expected text patterns. For security-sensitive file handling, checking the extension alone is not enough to validate a file.

#### D. Finding a position using `find()`

The `find()` method returns the index of the first occurrence of a substring. If the substring is not found, it returns `-1`.

```python
message = "I love Python programming with Python"

print(message.find("Python"))
print(message.find("Java"))
```

Output:

```text
7
-1
```

Remember that Python string indexes start at `0`.

#### E. Counting occurrences using `count()`

The `count()` method returns the number of non-overlapping occurrences of a substring.

```python
message = "I love Python programming with Python"

print(message.count("Python"))
print(message.count("o"))
```

Output:

```text
2
4
```

### 7. Replacing Text

The `replace()` method creates a new string with matching occurrences replaced.

```python
message = "I love Python programming with Python"

new_message = message.replace("Python", "JavaScript")

print(new_message)
```

Output:

```text
I love JavaScript programming with JavaScript
```

You can also limit the number of replacements.

```python
message = "Python is great. Python is useful."

print(message.replace("Python", "Java", 1))
```

Output:

```text
Java is great. Python is useful.
```

The third argument, `1`, limits the replacement to one occurrence.

**Important:** Python strings are immutable. String methods such as `replace()`, `upper()`, and `strip()` do not change the original string. They return a new string.

```python
text = "python"

text.upper()

print(text)
```

Output:

```text
python
```

To keep the transformed value, assign the result to a variable:

```python
text = "python"

text = text.upper()

print(text)
```

Output:

```text
PYTHON
```

### 8. Splitting and Joining Strings

Two especially useful string methods are `split()` and `join()`.

#### A. Splitting strings with `split()`

The `split()` method divides a string into a list of smaller strings.

```python
message = "Python is easy to learn"

words = message.split()

print(words)
```

Output:

```text
['Python', 'is', 'easy', 'to', 'learn']
```

By default, `split()` separates text using whitespace.

You can also specify a separator.

```python
tools = "Linux,Docker,Kubernetes"

tool_list = tools.split(",")

print(tool_list)
```

Output:

```text
['Linux', 'Docker', 'Kubernetes']
```

#### B. Joining strings with `join()`

The `join()` method combines strings from an iterable using a chosen separator.

```python
tools = ["Linux", "Docker", "Kubernetes"]

result = ", ".join(tools)

print(result)
```

Output:

```text
Linux, Docker, Kubernetes
```

You can use different separators:

```python
words = ["Python", "for", "AI"]

print(" ".join(words))
print("-".join(words))
```

Output:

```text
Python for AI
Python-for-AI
```

**Remember:** `split()` turns a string into a list, while `join()` combines strings from an iterable into one string.

### 9. Common Mistakes to Avoid

**Mistake 1: Forgetting the `f` in an f-string**

Incorrect:

```python
name = "Jane"

print("Hello, {name}!")
```

Output:

```text
Hello, {name}!
```

Without the `f` prefix, Python treats `{name}` as ordinary text.

Correct:

```python
name = "Jane"

print(f"Hello, {name}!")
```

Output:

```text
Hello, Jane!
```

**Mistake 2: Using incompatible quotation marks**

Incorrect:

```python
# message = "It's Python!'
```

This produces a `SyntaxError`.

Correct:

```python
message = "It's Python!"
print(message)
```

**Mistake 3: Expecting string methods to modify the original value**

Incorrect:

```python
text = "hello"
text.upper()

print(text)
```

Output:

```text
hello
```

Correct:

```python
text = "hello"
text = text.upper()

print(text)
```

Output:

```text
HELLO
```

**Mistake 4: Confusing `find()` with an error**

```python
text = "Python"

print(text.find("Java"))
```

Output:

```text
-1
```

A result of `-1` means the substring was not found. If you need a method that raises an error when the substring is missing, Python also provides `index()`.

### 10. Practical Exercise

Create a file named `string_manipulation.py` and complete the following tasks.

**Task 1: Format a greeting**

Create variables for a person's first name and age. Use an f-string to display a message such as:

`Hello, Jane! You are 25 years old.`

**Task 2: Clean user input**

Given the following string, remove extra whitespace from the beginning and end, then convert it to lowercase.

```python
username = "   Vaithee82   "
```

Expected result:

```text
vaithee82
```

**Task 3: Search and replace**

Given this sentence:

```python
message = "Python is useful. Python is powerful."
```

- Count how many times `"Python"` occurs.
- Check whether the sentence starts with `"Python"`.
- Replace `"Python"` with `"AI"`.

**Task 4: Split and join**

Convert this comma-separated string into a list, then join the values with a hyphen.

```python
tools = "Linux,Docker,Kubernetes"
```

Expected result:

```text
Linux-Docker-Kubernetes
```

**Task 5: Extract information from a log message**

Given:

```python
log_message = "ERROR: Database connection failed"
```

- Check whether the message starts with `"ERROR"`.
- Find the position of `"Database"`.
- Replace `"ERROR"` with `"WARNING"`.
- Print the final message.

### 11. Sample Solution

```python
# Task 1: Format a greeting
name = "Jane"
age = 25

print(f"Hello, {name}! You are {age} years old.")

# Task 2: Clean user input
username = "   Vaithee82   "

username = username.strip().lower()

print(username)

# Task 3: Search and replace
message = "Python is useful. Python is powerful."

print(message.count("Python"))
print(message.startswith("Python"))

updated_message = message.replace("Python", "AI")
print(updated_message)

# Task 4: Split and join
tools = "Linux,Docker,Kubernetes"

tool_list = tools.split(",")
result = "-".join(tool_list)

print(result)

# Task 5: Process a log message
log_message = "ERROR: Database connection failed"

print(log_message.startswith("ERROR"))
print(log_message.find("Database"))

updated_log = log_message.replace("ERROR", "WARNING")
print(updated_log)
```

Expected output:

```text
Hello, Jane! You are 25 years old.
vaithee82
2
True
AI is useful. AI is powerful.
Linux-Docker-Kubernetes
True
7
WARNING: Database connection failed
```

### 12. Summary

In this lesson, you learned how to:

- Combine strings using `+` and f-strings.
- Repeat text using `*`.
- Change letter case with `lower()`, `upper()`, and `title()`.
- Remove surrounding whitespace using `strip()`.
- Search for text using `in`, `find()`, `count()`, `startswith()`, and `endswith()`.
- Replace text using `replace()`.
- Split strings into lists and combine strings using `split()` and `join()`.
- Avoid common string manipulation errors.

### What's Next?

Now that you can manipulate text, let's learn **Conditional Statements in Python** — how to use `if`, `elif`, and `else` to make programs take different actions based on conditions.
