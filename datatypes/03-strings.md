# Strings in Python
## Working with Text in Python

### 1. What Are Strings?

A **string** is a sequence of characters used to represent text in Python. Strings can contain letters, numbers, spaces, symbols, and punctuation marks.

Strings are useful for storing names, messages, email addresses, file paths, and other text-based information.

Examples:

```python
name = "Alice"
message = "Hello, World!"
city = "Bengaluru"
```

In Python, the data type for strings is `str`.

```python
print(type(name))
print(type(message))
```

Output:

```text
<class 'str'>
<class 'str'>
```

**Important:** If you want Python to treat something as text, enclose it in quotation marks.

```python
age = 25       # Integer
age_text = "25"  # String

print(type(age))
print(type(age_text))
```

Output:

```text
<class 'int'>
<class 'str'>
```

Although both values contain `25`, they have different data types.

### 2. Creating Strings

Python provides three common ways to create strings.

#### A. Single quotes

Enclose text in single quotation marks.

```python
first = 'Python'
message = 'Welcome to Python'
print(first)
print(message)
```

Output:

```text
Python
Welcome to Python
```

#### B. Double quotes

You can also use double quotation marks.

```python
language = "Python"
message = "Hello, World!"

print(language)
print(message)
```

Output:

```text
Python
Hello, World!
```

Single and double quotes work the same way for ordinary strings. Choose the style that makes your code easy to read.

#### C. Triple quotes

Triple quotes allow you to create strings that span multiple lines.

You can use either triple single quotes (`'''`) or triple double quotes (`"""`).

```python
paragraph = """Python is easy to learn.
It is widely used in automation.
It is also popular in AI development."""

print(paragraph)
```

Output:

```text
Python is easy to learn.
It is widely used in automation.
It is also popular in AI development.
```

Triple-quoted strings are useful for multi-line text and documentation strings (docstrings).

#### Handling apostrophes inside strings

If your text contains an apostrophe, double quotes can make the string easier to write.

```python
message = "It's a beautiful day!"
print(message)
```

Output:

```text
It's a beautiful day!
```

You can also use single quotes by escaping the apostrophe with a backslash.

```python
message = 'It\'s a beautiful day!'
print(message)
```

Output:

```text
It's a beautiful day!
```

### 3. Combining Strings

Combining strings is called **string concatenation**.

Python uses the `+` operator to join strings together.

```python
first_name = "John"
last_name = "Doe"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
John Doe
```

The `" "` string adds a space between the first and last names.

Without the space, the result would be `JohnDoe`.

#### Repeating strings

You can use the `*` operator to repeat a string a specified number of times.

```python
stars = "*" * 5
print(stars)

message = "Hello! " * 3
print(message)
```

Output:

```text
*****
Hello! Hello! Hello!
```

This is useful for generating simple separators, repeated symbols, and sample text.

### 4. Finding the Length of a String

Python provides the built-in `len()` function to count the number of characters in a string.

```python
message = "Hello"
print(len(message))
```

Output:

```text
5
```

Spaces and punctuation marks also count as characters.

```python
message = "Hello World!"
print(len(message))
```

Output:

```text
12
```

Let's look at an empty string.

```python
empty = ""
print(len(empty))
```

Output:

```text
0
```

An empty string contains no characters.

### 5. Converting Values into Strings

Sometimes you need to convert a number or another value into text. Python provides the `str()` function for this purpose.

Example:

```python
age = 25

message = "I am " + str(age) + " years old."

print(message)
```

Output:

```text
I am 25 years old.
```

Here, `str(age)` converts the integer `25` into the string `"25"` so that it can be concatenated with other strings.

#### A simpler approach: f-strings

Python also supports **formatted string literals**, commonly called f-strings. They allow you to insert variables and expressions directly into a string.

Place the letter `f` before the opening quotation mark and put variables inside curly braces (`{}`).

```python
name = "Alice"
age = 25

message = f"My name is {name} and I am {age} years old."

print(message)
```

Output:

```text
My name is Alice and I am 25 years old.
```

You can also include calculations inside the curly braces.

```python
price = 100
quantity = 3

print(f"Total price: {price * quantity}")
```

Output:

```text
Total price: 300
```

F-strings are usually more readable than joining many strings with `+`. You will explore them in more detail later.

### 6. Accessing Individual Characters

Strings are sequences of characters. Python lets you access individual characters using their index.

**Indexing starts at `0`, not `1`.**

```python
language = "Python"

print(language[0])
print(language[1])
print(language[2])
```

Output:

```text
P
y
t
```

You can also access characters from the end using negative indexes.

```python
language = "Python"

print(language[-1])
print(language[-2])
```

Output:

```text
n
o
```

| Index | Character |
|---:|---|
| `0` | `P` |
| `1` | `y` |
| `2` | `t` |
| `3` | `h` |
| `4` | `o` |
| `5` or `-1` | `n` |

### 7. Common String Mistakes

#### Mistake 1: Mixing quotation marks incorrectly

Incorrect:

```python
message = "Hello'
```

This produces a `SyntaxError` because the opening and closing quotation marks do not match.

Correct:

```python
message = "Hello"
print(message)
```

#### Mist
