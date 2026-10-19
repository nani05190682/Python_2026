# Python Functions
## Create Reusable Blocks of Code

### 1. What Are Functions?

A **function** is a reusable block of code designed to perform a specific task. Instead of writing the same code repeatedly, you can write it once inside a function and call it whenever you need it.

Think of a function as a machine: you provide input, the machine performs an operation, and it may produce output.

**Real-world examples:**

- A coffee machine takes your selection and prepares a drink.
- A calculator takes numbers and performs calculations.
- A login system checks a username and password.
- A monitoring script checks whether a server is running.

In Python, functions help you organize code into smaller, manageable pieces.

### 2. Why Do We Need Functions?

Functions provide several important benefits.

**1. Avoid repetition**

Write code once and reuse it whenever required.

**2. Improve readability**

Divide a large program into smaller, meaningful tasks.

**3. Simplify maintenance**

If you need to change a task's implementation, you can update the function in one place.

**4. Improve testing**

You can test individual functions separately to identify problems more easily.

**5. Encourage reusability**

A function can be called multiple times with different inputs.

### 3. Real-World Examples of Python Functions

Python includes many built-in functions that you can use immediately.

```python
print("Hello, Python!")
```

The `print()` function displays information.

```python
numbers = [10, 20, 30, 40]

print(len(numbers))
```

Output:

```text
4
```

The `len()` function returns the number of elements in the list.

Python also allows you to create your own functions, such as:

- `calculate_tax()` — calculate tax.
- `check_server_status()` — check a server's status.
- `send_email()` — send an email.
- `calculate_average()` — calculate an average.

These are examples of custom function names. Their behavior depends on the code you write inside them.

### 4. What You'll Learn

In this lesson series, you'll explore:

1. Creating functions using `def`.
2. Calling functions.
3. Passing arguments and parameters.
4. Returning values using `return`.
5. Using default and keyword arguments.
6. Understanding local and global variables.
7. Writing functions with flexible arguments.
8. Using lambda functions.
9. Applying functions to practical Python automation tasks.

### 5. Your First Python Function

Let's begin by creating a simple function.

```python
def greet():
    print("Hello, welcome to Python!")

greet()
```

Output:

```text
Hello, welcome to Python!
```

Let's understand each part:

- `def` is the Python keyword used to define a function.
- `greet` is the function's name.
- `()` contains the parameters, if any.
- `:` marks the beginning of the function body.
- The indented statement is the code executed by the function.
- `greet()` calls the function and runs its code.

**Important:** Defining a function does not execute its body. The body runs when you call the function.

### 6. Your First Practice Task

Create a function named `welcome()` that prints:

```text
Welcome to Python programming!
```

Then call the function to execute it.

Once you understand how to define and call functions, you're ready to learn how to pass information into them using parameters and arguments.

### What's Next?

**Creating Functions with `def` — Define and Call Your Own Functions**

You'll learn the function syntax in detail, how indentation works, and how to call a function multiple times without repeating the code.
