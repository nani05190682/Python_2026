# When to Use Python Classes — Best Practices and Guidelines

## 1. Introduction

You have learned how to create classes, initialize objects, define attributes and methods, and use inheritance.

But an important question remains:

**When should you use a class, and when is a simple function enough?**

Python supports multiple programming styles. Two common approaches are:

- **Functional programming:** Organizing code around functions that transform data and produce results.
- **Object-oriented programming (OOP):** Organizing code around objects that combine related data and behavior.

Both approaches are useful. The goal is not to use classes everywhere, but to choose the approach that makes your code easier to understand, test, maintain, and extend.

By the end of this lesson, you will understand when to use classes, when to use functions, common design mistakes, and how to make better decisions when building Python applications.

## 2. Programming Paradigms

A programming paradigm is a general approach to organizing and writing code.

Let's compare functional and object-oriented styles using a text-processing example.

### 2.1 Functional approach

Functions take input, perform operations, and return results.

```python
def clean_text(text):
    return text.strip().lower()


def remove_punctuation(text):
    return text.replace(".", "").replace(",", "")


text = "  Hello, World.  "

result = remove_punctuation(clean_text(text))

print(result)
```

Output:

```text
hello world
```

Each function has one responsibility:

- `clean_text()` removes surrounding whitespace and converts the text to lowercase.
- `remove_punctuation()` removes periods and commas.
- The result of one function becomes the input to another.

The original string is not modified because strings are immutable. Each function returns a new string.

### 2.2 Object-oriented approach

With OOP, we can bundle the text and its processing operations into one object.

```python
class TextProcessor:
    def __init__(self, text):
        self.text = text

    def clean(self):
        self.text = self.text.strip().lower()
        return self

    def remove_punctuation(self):
        self.text = self.text.replace(".", "").replace(",", "")
        return self


processor = TextProcessor("  Hello, World.  ")

result = processor.clean().remove_punctuation().text

print(result)
```

Output:

```text
hello world
```

In this version:

- `TextProcessor` is the class.
- `self.text` stores the current text.
- `clean()` modifies the object's state.
- `remove_punctuation()` modifies the same object.
- `return self` allows the methods to be chained.

### 2.3 Comparing the two approaches

| Functional approach | Object-oriented approach |
|---|---|
| Uses standalone functions | Uses methods defined in classes |
| Passes data between operations | Can retain data inside objects |
| Often simpler for stateless transformations | Useful when data and behavior belong together |
| Makes data flow explicit | Can maintain state between operations |

Both approaches can solve the same problem. Neither is automatically better.

**Important:** Classes do not unlock capabilities that functions cannot provide. They offer a different way to organize code, and Python applications often combine both styles.

## 3. When Should You Use Classes?

Classes are particularly useful when your application needs to manage state, represent multiple related objects, or provide a cohesive interface.

### Use Case 1: Maintaining state

State is the information an object stores and updates over time.

For example, an API client might need to track how many requests it has made.

```python
class APIClient:
    def __init__(self, base_url):
        self.base_url = base_url
        self.request_count = 0

    def record_request(self):
        self.request_count += 1

    def show_status(self):
        print(f"API URL: {self.base_url}")
        print(f"Requests: {self.request_count}")


client = APIClient("https://api.example.com")

client.record_request()
client.record_request()

client.show_status()
```

Output:

```text
API URL: https://api.example.com
Requests: 2
```

The object remembers its request count between method calls.

A class is useful here because the URL and request count belong to the same client.

### Use Case 2: Grouping related data and behavior

Suppose you are building an SRE tool that monitors server CPU usage.

A server has data, such as its hostname and CPU usage, and behavior, such as checking its health.

```python
class Server:
    def __init__(self, hostname, cpu_usage):
        self.hostname = hostname
        self.cpu_usage = cpu_usage

    def check_health(self):
        if self.cpu_usage >= 90:
            return "WARNING"

        return "OK"


server = Server("web-01", 95)

print(server.hostname)
print(server.check_health())
```

Output:

```text
web-01
WARNING
```

The class groups related information and behavior into one understandable unit.

### Use Case 3: Creating multiple objects

Classes are helpful when you need many objects with the same structure but different data.

```python
class Server:
    def __init__(self, hostname, environment):
        self.hostname = hostname
        self.environment = environment

    def describe(self):
        return f"{self.hostname} ({self.environment})"


servers = [
    Server("web-01", "production"),
    Server("web-02", "production"),
    Server("web-dev-01", "development")
]

for server in servers:
    print(server.describe())
```

Output:

```text
web-01 (production)
web-02 (production)
web-dev-01 (development)
```

You define the structure once and create as many server objects as necessary.

### Use Case 4: Building reusable components

Classes can provide a consistent interface for larger components, such as:

- API clients
- Database connections
- Data processors
- Cloud resource managers
- AI model wrappers
- Monitoring agents

For example, an AI application might have an `AIClient` class that stores model configuration and provides methods for sending prompts, handling responses, and managing request settings.

For production systems, credentials should be loaded securely rather than hardcoded in the class.

## 4. When Should You Use Functions Instead?

Functions are often the better choice when the operation is simple, independent, and does not need to maintain state.

### Use Case 1: Simple transformations

```python
def convert_to_uppercase(text):
    return text.upper()


print(convert_to_uppercase("python"))
```

Output:

```text
PYTHON
```

Creating a class solely to uppercase a string would usually add unnecessary complexity.

### Use Case 2: Calculations

```python
def calculate_total(price, quantity):
    return price * quantity


print(calculate_total(500, 3))
```

Output:

```text
1500
```

This function takes inputs, calculates a result, and returns it. It does not need to remember anything between calls.

### Use Case 3: Small scripts

```python
def main():
    name = input("Enter your name: ")
    print(f"Hello, {name}!")


if __name__ == "__main__":
    main()
```

A small script can be perfectly well organized with a few functions. There is no need to introduce classes unless they solve a real problem.

### Use Case 4: Reusable utilities

Functions are ideal for reusable operations such as:

- Formatting strings
- Validating a value
- Converting units
- Parsing a small data structure
- Calculating statistics
- Converting temperatures

**Rule of thumb:** Start with functions when they are sufficient. Introduce classes when the data, behavior, or state naturally belong together.

## 5. Functions vs. Classes: A Practical Comparison

| Requirement | Usually a good starting point |
|---|---|
| Calculate a total | Function |
| Convert Celsius to Fahrenheit | Function |
| Clean a string | Function |
| Track a server's changing status | Class |
| Manage multiple API clients with separate configuration | Class |
| Store and update a shopping cart | Class |
| Process a file once | Function |
| Maintain a long-lived connection or session | Class or a suitable context-managed object |

These are guidelines, not strict rules. For example, a data-processing application can use functions for transformations and classes for managing its configuration or processing pipeline.

## 6. Common Design Pitfalls

### Pitfall 1: Over-engineering

Over-engineering means adding unnecessary complexity to a solution.

Consider this example:

```python
class Calculator:
    def add(self, a, b):
        return a + b


calculator = Calculator()

print(calculator.add(10, 20))
```

This code works, but if the only requirement is to add two numbers, a function is simpler:

```python
def add(a, b):
    return a + b


print(add(10, 20))
```

Do not create a class simply because you are learning OOP.

A class with one method is not automatically bad. It can be appropriate when the object represents a meaningful component, implements an interface, or needs to manage state. The question is whether the class adds clarity or useful structure.

### Pitfall 2: God objects

A *god object* is a class that takes on too many unrelated responsibilities.

For example, imagine a single class responsible for:

- Calling AI APIs
- Managing user accounts
- Processing CSV files
- Monitoring Linux servers
- Sending email alerts
- Generating reports

This class would be difficult to test, maintain, and extend.

A better design separates responsibilities:

```python
class AIClient:
    def generate(self, prompt):
        # AI API interaction belongs here.
        pass


class ServerMonitor:
    def check_health(self, hostname):
        # Server monitoring belongs here.
        pass


class ReportGenerator:
    def generate_report(self, data):
        # Report formatting belongs here.
        pass
```

These are illustrative method stubs, not complete implementations.

Each class has a more focused responsibility.

### Pitfall 3: Creating classes containing only static methods

A class that contains only `@staticmethod` methods and no meaningful shared state or object behavior may be unnecessary.

For example:

```python
class TextUtils:
    @staticmethod
    def clean(text):
        return text.strip().lower()

    @staticmethod
    def uppercase(text):
        return text.upper()
```

If these operations are independent utilities, a module containing functions is often simpler:

```python
def clean(text):
    return text.strip().lower()


def uppercase(text):
    return text.upper()
```

You can save these functions in `text_utils.py` and import them elsewhere:

```python
from text_utils import clean, uppercase

print(clean("  Python  "))
print(uppercase("python"))
```

Output:

```text
python
PYTHON
```

Static methods still have legitimate uses, especially when a function logically belongs to a class but does not need an instance or class state. The goal is to avoid unnecessary structure, not to avoid static methods entirely.

### Pitfall 4: Inheritance without a meaningful relationship

Inheritance should represent a genuine relationship between types.

For example, a `Dog` is an `Animal`, so inheriting from `Animal` makes sense.

A `Car` is not an `Engine`. A car *has an* engine, so composition is usually more appropriate.

Use inheritance when the relationship and shared behavior are meaningful. Use composition when an object needs to contain or collaborate with another object.

## 7. Best Practices for Writing Maintainable Classes

Follow these guidelines when designing Python classes.

1. **Keep classes focused.** Give each class a clear responsibility.
2. **Start simple.** Use functions and basic data structures until a class offers a clear advantage.
3. **Use descriptive names.** Class names normally use `PascalCase`, such as `ServerMonitor`. Function and method names normally use `snake_case`, such as `check_health`.
4. **Initialize required attributes.** Set up the state an object needs before its methods depend on it.
5. **Avoid unnecessary shared mutable state.** Be careful with class-level lists and dictionaries.
6. **Prefer composition when appropriate.** An object can use another object without inheriting from it.
7. **Keep functions and methods small and understandable.** Each should perform a clear task.
8. **Write tests.** Verify normal behavior, invalid input, and important edge cases.
9. **Avoid premature abstraction.** Do not introduce complex inheritance hierarchies for problems that have not yet appeared.
10. **Refactor when repetition becomes meaningful.** If several functions repeatedly use the same configuration and state, consider whether a class would make the design clearer.

## 8. Practice Exercises

Try these exercises before checking the solutions.

### Exercise 1: Function or class?

For each requirement, decide whether you would start with a function or a class. Explain why.

1. Convert a temperature from Celsius to Fahrenheit.
2. Maintain a shopping cart containing multiple items.
3. Convert a string to lowercase.
4. Track CPU utilization and health status for several servers.
5. Calculate the total price of a list of products.

### Exercise 2: Refactor an unnecessary class

Rewrite the following code using a simple function.

```python
class StringFormatter:
    def uppercase(self, text):
        return text.upper()


formatter = StringFormatter()

print(formatter.upper("hello"))
```

### Exercise 3: Design a focused class

Create a `ServerMonitor` class that:

- Stores a hostname and CPU usage.
- Provides a `check_health()` method.
- Returns `"WARNING"` when CPU usage is at least 90%.
- Returns `"OK"` otherwise.

Avoid adding unrelated functionality.

### Exercise 4: Separate responsibilities

You are building a monitoring application. One class currently manages server health, formats reports, and sends email notifications.

Suggest three focused components and describe what each should do.

## 9. Exercise Solutions

### Solution 1: Function or class?

1. **Temperature conversion — Function.** It is a straightforward calculation without persistent state.
2. **Shopping cart — Class.** It can maintain a collection of items and provide operations such as adding and removing products.
3. **Lowercase conversion — Function.** It is a simple transformation.
4. **Server monitoring — Class or a combination of classes and functions.** A server object can maintain its own data, while standalone functions can perform independent calculations.
5. **Total price — Function.** It is usually a straightforward calculation over supplied data.

### Solution 2: Refactor the class

```python
def uppercase(text):
    return text.upper()


print(uppercase("hello"))
```

Output:

```text
HELLO
```

### Solution 3: Focused server monitor

```python
class ServerMonitor:
    def __init__(self, hostname, cpu_usage):
        self.hostname = hostname
        self.cpu_usage = cpu_usage

    def check_health(self):
        if self.cpu_usage >= 90:
            return "WARNING"

        return "OK"


server = ServerMonitor("web-01", 95)

print(server.check_health())
```

Output:

```text
WARNING
```

For production code, add input validation and obtain CPU utilization from a real monitoring source.

### Solution 4: Separate responsibilities

A reasonable design would be:

- `ServerMonitor` — Collects or evaluates server health information.
- `ReportGenerator` — Formats collected data into reports.
- `EmailNotifier` — Sends notifications through an email service.

These components can collaborate without requiring one class to manage every responsibility.

## 10. Summary

In this lesson, you learned that Python supports multiple programming styles and that classes are one way to organize code.

Use **functions** when operations are independent, stateless, and straightforward.

Use **classes** when you need to combine related data and behavior, maintain object state, or create multiple objects with a consistent interface.

Avoid over-engineering, god objects, unnecessary inheritance, and classes that provide no meaningful organizational benefit.

**The most important principle is simplicity:** choose the design that makes your code easiest to understand, test, and maintain.

## 11. What's Next?

Next, you will learn **Git and GitHub — Track Your Code Changes Professionally**.

You will explore version control, repositories, commits, branches, and how to store and collaborate on Python projects using Git and GitHub.
