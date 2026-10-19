# Control Flow in Python
## Make Your Programs Smart with Decisions

### 1. Introduction to Control Flow

So far, you have learned how to store data in variables, perform calculations, work with strings, and compare values.

But what happens when a program needs to make a decision?

For example:
- Should an application allow a user to log in?
- Should an ATM dispense cash?
- Should a monitoring system report a server as healthy or unhealthy?
- Should a game continue or display a game-over message?

Programs need a way to choose what happens next based on specific conditions. This is where **control flow** comes in.

Control flow determines the order in which instructions are executed in a program.

By default, Python executes statements from top to bottom. Control flow statements allow a program to make decisions, repeat actions, or change the normal execution sequence.

### 2. Real-World Examples

Decision-making is part of almost every application.

| Real-world scenario | Example condition | Action |
|---|---|---|
| ATM | PIN is correct | Allow access |
| Login application | Password is valid | Continue login |
| Weather application | Temperature is below a threshold | Display an appropriate weather message |
| Game | Player health reaches zero | Display game over |
| Server monitoring | Health check fails | Report an unhealthy server |

These examples follow a simple pattern:

**Condition → Decision → Action**

For example, a server monitoring program might check whether a service is responding. If the health check succeeds, it reports the service as healthy; otherwise, it reports a failure.

### 3. Types of Control Flow in Python

Python provides several ways to control program execution.

**1. Conditional statements**

Used to make decisions based on conditions.

- `if`
- `elif`
- `else`

**2. Loops**

Used to repeat instructions.

- `for`
- `while`

**3. Loop control statements**

Used to change how a loop executes.

- `break`
- `continue`
- `pass`

In this section, you will begin with conditional statements and gradually learn how to build more advanced programs.

### 4. How Conditions Work

A condition is an expression that evaluates to `True` or `False`.

For example:

```python
age = 20

print(age >= 18)
print(age < 18)
```

Output:

```text
True
False
```

Python evaluates each comparison and produces a Boolean result.

These results can be used to decide which instructions should execute.

### 5. Prerequisites

Before starting this section, make sure you understand:

- Variables and basic data types (`int`, `float`, `str`, and `bool`).
- Arithmetic and comparison operators.
- Boolean values (`True` and `False`).
- Logical operators (`and`, `or`, and `not`).
- How to run a Python program in VS Code.

### 6. Learning Objectives

By the end of this section, you will be able to:

- Explain how control flow works.
- Use `if` statements to execute code conditionally.
- Use `if-else` statements to choose between two alternatives.
- Use `if-elif-else` statements to handle multiple conditions.
- Combine conditions using logical operators.
- Build simple decision-making programs using real-world examples.

### 7. Your First Decision-Making Program

Let's start with a simple example.

```python
age = 20

if age >= 18:
    print("You are eligible to vote.")
```

Output:

```text
You are eligible to vote.
```

Python checks whether `age >= 18`. Because the condition is `True`, it executes the indented `print()` statement.

If the condition is `False`, Python skips the statement inside the `if` block.

You will explore the syntax and behavior of `if` statements in the next lesson.

### What's Next?

**Lesson 1: If Statements in Python**

Learn how to use `if` statements to make decisions and execute code only when a condition is satisfied.
