# Python Function Parameters and Arguments
## Pass Data into Your Functions

### 1. What Are Parameters?

Parameters allow you to pass data into functions, making them flexible and reusable. Instead of hardcoding a value inside a function, you can provide different inputs whenever you call it.

Imagine you are building a server monitoring tool. Instead of creating a separate function for every server, you can create one function that accepts a server name as input.

**Without parameters:**

```python
def greet_alice():
    print("Hello, Alice!")

greet_alice()
```

Output:

```text
Hello, Alice!
```

This function always greets Alice. To greet another person, you would need to change the function or create another one.

**With parameters:**

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
greet("Bob")
greet("Charlie")
```

Output:

```text
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

Now the same function works for different people.

**Key takeaway:** Parameters make functions reusable by allowing them to accept different inputs.

### 2. Parameters vs. Arguments

Although people sometimes use these terms interchangeably, parameters and arguments have different meanings.

- **Parameter:** A variable listed in the function definition.
- **Argument:** The actual value supplied when the function is called.

Example:

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

In this example:

- `name` is the parameter.
- `"Alice"` is the argument.
- `greet("Alice")` is the function call.

Think of a parameter as an input placeholder and an argument as the actual input value.

### 3. Creating Functions with Parameters

You define parameters inside the parentheses in a function definition.

Syntax:

```python
def function_name(parameter):
    # Function body
    statements
```

Example:

```python
def display_message(message):
    print(message)

display_message("Welcome to Python!")
display_message("Learning functions is easy.")
```

Output:

```text
Welcome to Python!
Learning functions is easy.
```

The function receives a value through `message` and displays it.

### 4. Using Multiple Parameters

A function can accept multiple parameters separated by commas.

Example:

```python
def introduce(name, age):
    print(f"My name is {name}.")
    print(f"I am {age} years old.")

introduce("Alice", 25)
introduce("Bob", 30)
```

Output:

```text
My name is Alice.
I am 25 years old.
My name is Bob.
I am 30 years old.
```

Python assigns the arguments to parameters according to their positions.

For example, in `introduce("Alice", 25)`:

- `"Alice"` is assigned to `name`.
- `25` is assigned to `age`.

### 5. Understanding Positional Arguments

Positional arguments are assigned to parameters based on their order in the function call.

```python
def describe_server(hostname, ip_address, status):
    print(f"Hostname: {hostname}")
    print(f"IP address: {ip_address}")
    print(f"Status: {status}")

describe_server("web01", "192.168.1.10", "running")
```

Output:

```text
Hostname: web01
IP address: 192.168.1.10
Status: running
```

The first argument goes to `hostname`, the second to `ip_address`, and the third to `status`.

**Important:** The order matters when using positional arguments.

For example:

```python
describe_server("192.168.1.10", "web01", "running")
```

This call is valid Python, but it assigns the IP address to `hostname` and the hostname to `ip_address`. The output would be logically incorrect.

### 6. Practical Example: Calculating a Total

Let's create a function that calculates a price after tax and discount.

```python
def calculate_total(price, tax_rate, discount):
    tax = price * tax_rate
    final_price = price + tax - discount

    print(f"Total: ${final_price:.2f}")

calculate_total(100, 0.08, 10)
```

Output:

```text
Total: $98.00
```

Let's understand the calculation:

- Price = `$100`
- Tax rate = `8%`
- Tax = `$100 × 0.08 = $8`
- Discount = `$10`
- Final total = `$100 + $8 - $10 = $98`

You can call the same function with different inputs:

```python
calculate_total(200, 0.10, 20)
calculate_total(500, 0.05, 15)
```

Output:

```text
Total: $200.00
Total: $510.00
```

This example demonstrates how parameters allow a function to perform the same operation with different values.

### 7. Default Parameter Values

Sometimes, you want a parameter to have a default value. This allows callers to omit that argument when the default is appropriate.

Example:

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")
greet("Bob", "Hi")
greet("Charlie", "Hey")
```

Output:

```text
Hello, Alice!
Hi, Bob!
Hey, Charlie!
```

When you call `greet("Alice")`, Python uses the default value `"Hello"` for `greeting`.

When you call `greet("Bob", "Hi")`, the supplied argument overrides the default.

#### Another example: Server monitoring

```python
def check_service(service_name, status="running"):
    print(f"{service_name}: {status}")

check_service("nginx")
check_service("mysql", "stopped")
```

Output:

```text
nginx: running
mysql: stopped
```

The first call uses the default status. The second call provides a different status.

#### Rule for default parameters

Parameters without defaults must come before parameters with defaults.

Correct:

```python
def create_user(name, role="user"):
    print(f"{name}: {role}")
```

Incorrect:

```python
def create_user(role="user", name):
    print(f"{name}: {role}")
```

The second definition raises a `SyntaxError` because a required parameter follows a default parameter.

### 8. Keyword Arguments

Keyword arguments let you specify which parameter receives each value by using the parameter name.

Example:

```python
def create_profile(name, age, city):
    print(f"{name}, {age}, from {city}")

create_profile(name="Alice", age=25, city="New York")
```

Output:

```text
Alice, 25, from New York
```

You can also provide keyword arguments in a different order:

```python
create_profile(city="New York", age=25, name="Alice")
```

Output:

```text
Alice, 25, from New York
```

Python matches each value to the parameter name rather than its position.

#### Positional vs. keyword arguments

| Feature | Positional arguments | Keyword arguments |
|---|---|---|
| Assignment | Based on order | Based on parameter name |
| Order | Matters | Can vary |
| Example | `greet("Alice")` | `greet(name="Alice")` |
| Readability | Simple for short calls | Often clearer for multiple inputs |

You can combine positional and keyword arguments, but positional arguments must come before keyword arguments.

Correct:

```python
create_profile("Alice", age=25, city="New York")
```

Incorrect:

```python
create_profile(name="Alice", 25, city="New York")
```

The second call raises a `SyntaxError` because a positional argument follows a keyword argument.

### 9. Common Mistakes

#### Mistake 1: Providing the wrong number of arguments

```python
def add_numbers(a, b):
    print(a + b)

add_numbers(10)
```

Output:

```text
TypeError
```

The function requires two arguments, but only one was provided.

Correct:

```python
add_numbers(10, 20)
```

Output:

```text
30
```

#### Mistake 2: Mixing up argument order

```python
def introduce(name, age):
    print(f"{name} is {age} years old.")

introduce(25, "Alice")
```

This code runs, but the output is logically incorrect:

```text
25 is Alice years old.
```

Python does not automatically validate that `name` is a string or `age` is a number.

Use the correct order or keyword arguments:

```python
introduce(name="Alice", age=25)
```

Output:

```text
Alice is 25 years old.
```

#### Mistake 3: Forgetting required arguments

```python
def greet(name):
    print(f"Hello, {name}!")

greet()
```

This raises a `TypeError` because the required `name` argument is missing.

Provide the argument:

```python
greet("Alice")
```

#### Mistake 4: Using mutable objects as default values

Avoid using mutable objects such as lists or dictionaries as default parameter values when you expect a fresh object for every call.

Problematic example:

```python
def add_item(item, items=[]):
    items.append(item)
    print(items)

add_item("apple")
add_item("banana")
```

Output:

```text
['apple']
['apple', 'banana']
```

Both calls use the same default list because Python evaluates the default argument once when the function is defined.

A safer approach is to use `None` as the default and create a new list inside the function.

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    print(items)

add_item("apple")
add_item("banana")
```

Output:

```text
['apple']
['banana']
```

Each call now gets its own list when no list is provided.

### 10. Practice Exercises

Try these exercises before checking the solutions.

**Exercise 1: Greeting function**

Create a function called `greet_user(name)` that prints a greeting. Call it with three different names.

**Exercise 2: Add two numbers**

Create a function called `add_numbers(a, b)` that prints the sum of two numbers.

**Exercise 3: Calculate a discount**

Create a function called `calculate_discount(price, discount)` that calculates and prints the final price after subtracting the discount.

**Exercise 4: Default parameter**

Create a function called `send_message(name, message="Welcome!")` that prints the message and the recipient's name.

**Exercise 5: Keyword arguments**

Create a function called `display_employee(name, role, city)` that displays employee information. Call it using keyword arguments in a different order from the function definition.

**Exercise 6: DevOps practical example**

Create a function called `check_server(hostname, status="running")` that prints the hostname and status.

Call it twice:

- First, provide only the hostname.
- Second, provide the hostname and `"stopped"` as the status.

### 11. Sample Solutions

#### Solution 1

```python
def greet_user(name):
    print(f"Hello, {name}!")

greet_user("Alice")
greet_user("Bob")
greet_user("Charlie")
```

#### Solution 2

```python
def add_numbers(a, b):
    print(a + b)

add_numbers(10, 20)
```

Output:

```text
30
```

#### Solution 3

```python
def calculate_discount(price, discount):
    final_price = price - discount
    print(f"Final price: {final_price:.2f}")

calculate_discount(100, 15)
```

Output:

```text
Final price: 85.00
```

#### Solution 4

```python
def send_message(name, message="Welcome!"):
    print(f"{message} {name}")

send_message("Alice")
send_message("Bob", "Good morning!")
```

Output:

```text
Welcome! Alice
Good morning! Bob
```

#### Solution 5

```python
def display_employee(name, role, city):
    print(f"{name} works as a {role} in {city}.")

display_employee(city="Bengaluru", name="Ravi", role="DevOps Engineer")
```

Output:

```text
Ravi works as a DevOps Engineer in Bengaluru.
```

#### Solution 6

```python
def check_server(hostname, status="running"):
    print(f"{hostname}: {status}")

check_server("web01")
check_server("db01", "stopped")
```

Output:

```text
web01: running
db01: stopped
```

### 12. Quick Summary

| Concept | Example | Purpose |
|---|---|---|
| Parameter | `def greet(name):` | Defines an input variable |
| Argument | `greet("Alice")` | Supplies a value to the function |
| Multiple parameters | `def add(a, b):` | Accepts multiple inputs |
| Default parameter | `def greet(name, message="Hi"):` | Provides an optional default |
| Positional argument | `add(10, 20)` | Assigns values by order |
| Keyword argument | `greet(name="Alice")` | Assigns values by name |
| Mutable default alternative | `items=None` | Avoids sharing a mutable default object |

**Key takeaway:** Parameters allow functions to work with different inputs instead of relying on hardcoded values. Use descriptive parameter names, provide the correct arguments, and choose default values carefully.

### What's Next?

**Return Values in Python — Get Results from Functions**

You'll learn how to use `return`, capture function results in variables, and distinguish between returning a value and printing it.
