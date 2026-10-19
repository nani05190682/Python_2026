# Introduction to Programming

## What Programming Really Means

### 1. What Is Programming?

Programming is the process of writing instructions that tell a computer how to perform a task.

Think of programming like writing a recipe. A recipe provides step-by-step instructions for preparing a meal. Similarly, a computer program provides instructions that a computer can execute to perform a specific task.

For example, a cooking recipe might say:

1. Heat the oil.
2. Add the onions.
3. Stir for two minutes.
4. Add the remaining ingredients.
5. Cook until ready.

A computer program follows the same general idea: it receives instructions and performs the specified operations.

The difference is that programming requires instructions to follow the precise syntax and rules of a programming language.

### 2. Computers Need Clear Instructions

Computers execute instructions according to the program's logic. They do not automatically understand vague intentions the way humans often do.

For example, if you ask a friend to make coffee, they may know which cup to use and how much sugar to add.

A computer-controlled coffee machine, however, needs explicit instructions about the required operations, such as:

1. Check whether water is available.
2. Heat the water.
3. Measure the coffee.
4. Brew the coffee.
5. Pour it into a cup.
6. Add milk or sugar if requested.

The exact steps depend on the machine and the task.

**Key concept:** A computer program must define the operations and decisions needed to achieve the desired result.

## 3. Basic Programming Operations

Most programs combine a few fundamental concepts. Let's explore them using simple Python examples.

### Example 1: Store Information Using Variables

Variables allow you to store information and use it later.

```python
name = "Sarah"
age = 25
city = "Bengaluru"

print(name)
print(age)
print(city)
```

**Output:**

```text
Sarah
25
Bengaluru
```

**Explanation:**

- `name` stores a person's name.
- `age` stores an integer.
- `city` stores a location.
- `print()` displays the values.

**Real-world application:** A student management system can store student names, ages, and course details in variables.

### Example 2: Make Decisions Using Conditions

Programs often need to make decisions based on specific conditions.

For example, an application might check whether a person is eligible to vote based on their age.

```python
age = 20

if age >= 18:
    print("You are eligible to vote.")
else:
    print("You are not yet eligible to vote.")
```

**Output:**

```text
You are eligible to vote.
```

**Explanation:**

- `if` checks whether a condition is true.
- `age >= 18` compares the person's age with 18.
- `else` provides an alternative when the condition is false.

**Real-world application:** Online forms can validate age requirements before allowing a user to continue.

### Example 3: Repeat Actions Using Loops

Loops allow you to execute the same instructions multiple times.

Imagine you need to display a message five times. Instead of writing five separate `print()` statements, you can use a loop.

```python
for number in range(1, 6):
    print("Welcome to Python!")
```

**Output:**

```text
Welcome to Python!
Welcome to Python!
Welcome to Python!
Welcome to Python!
Welcome to Python!
```

**Explanation:**

- `for` starts a loop.
- `range(1, 6)` generates the numbers 1 through 5.
- The indented statement executes once for each number.

**Real-world application:** Loops can process multiple files, check server statuses, or examine a list of application records.

### Example 4: Perform Calculations

Programs can perform mathematical calculations quickly and consistently.

For example, a shopping application might calculate the total price of a product and its tax.

```python
price = 1000
tax = 180

total = price + tax

print("Product price:", price)
print("Tax:", tax)
print("Total amount:", total)
```

**Output:**

```text
Product price: 1000
Tax: 180
Total amount: 1180
```

**Explanation:**

- `price` stores the product price.
- `tax` stores the tax amount.
- `+` adds the two values.
- `total` stores the calculated amount.

**Real-world application:** Billing systems use calculations to determine totals, discounts, taxes, and payment amounts.

## 4. Additional Real-World Programming Examples

### Example 5: Check Whether a Number Is Even or Odd

A program can use the remainder operator (`%`) to determine whether a number is even or odd.

```python
number = 12

if number % 2 == 0:
    print("The number is even.")
else:
    print("The number is odd.")
```

**Output:**

```text
The number is even.
```

**Explanation:** When a number is divided by 2, an even number has a remainder of zero.

### Example 6: Accept Input from a User

Programs can interact with users by accepting input.

```python
name = input("Enter your name: ")

print("Hello,", name)
print("Welcome to Python programming!")
```

**Example interaction:**

```text
Enter your name: Ravi
Hello, Ravi
Welcome to Python programming!
```

**Explanation:**

- `input()` displays a prompt and accepts text from the user.
- The entered text is stored in the `name` variable.
- `print()` displays a personalized message.

### Example 7: Check a Server Status

Programming is especially useful in DevOps and system administration because repetitive tasks can be automated.

```python
server_status = "running"

if server_status == "running":
    print("Server is healthy.")
else:
    print("Check the server immediately.")
```

**Output:**

```text
Server is healthy.
```

**Explanation:** The program compares the server status with the expected value and displays an appropriate message.

**Real-world application:** Monitoring scripts can inspect service states and generate alerts when a service is unavailable. A production monitoring system would obtain the status from an actual server or monitoring API rather than a hardcoded variable.

### Example 8: Process Multiple Servers

Suppose you need to display the status of several servers.

```python
servers = ["web01", "web02", "db01"]

for server in servers:
    print(server, "is being checked.")
```

**Output:**

```text
web01 is being checked.
web02 is being checked.
db01 is being checked.
```

**Explanation:** The loop processes each server name in the list.

**Real-world application:** Automation tools can iterate over server inventories to perform health checks, collect information, or execute approved maintenance tasks.

### Example 9: Create a Reusable Function

Functions let you group instructions into reusable blocks of code.

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Sarah")
greet("Ravi")
```

**Output:**

```text
Hello, Sarah!
Hello, Ravi!
```

**Explanation:**

- `def` defines a function.
- `greet` is the function name.
- `name` is a parameter.
- Calling `greet()` executes the function body.

**Real-world application:** Functions help organize code for tasks such as validating input, checking service status, or formatting reports.

## 5. How These Concepts Work Together

A complete program often combines variables, input, calculations, and decisions.

Consider this example of a simple shopping bill calculator.

```python
product_name = input("Enter the product name: ")
price = float(input("Enter the product price: "))
quantity = int(input("Enter the quantity: "))

total = price * quantity

print("\n--- Shopping Bill ---")
print("Product:", product_name)
print("Price:", price)
print("Quantity:", quantity)
print("Total:", total)

if total >= 1000:
    print("You qualify for a special offer!")
else:
    print("Thank you for shopping!")
```

**Example interaction:**

```text
Enter the product name: Keyboard
Enter the product price: 750
Enter the quantity: 2

--- Shopping Bill ---
Product: Keyboard
Price: 750.0
Quantity: 2
Total: 1500.0
You qualify for a special offer!
```

This example combines:

- Variables to store product information.
- `input()` to collect user data.
- `float()` and `int()` to convert input into numeric values.
- Arithmetic to calculate the total.
- Conditional statements to make a decision.
- `print()` to display the result.

## 6. Your Programming Journey

Programming may seem unfamiliar at first, but each concept builds on what you have already learned.

As you progress through Python Basics, you will learn how to:

- Store and manipulate information.
- Make decisions using conditions.
- Repeat tasks using loops.
- Organize code using functions.
- Work with files, APIs, and external services.
- Automate repetitive tasks.
- Build applications that use AI technologies.

Programming is a practical skill that improves with regular practice. Start with small programs, understand how they work, and gradually increase their complexity.

## 7. Practice Exercises

Try completing these exercises independently.

**Exercise 1: Personal Introduction**

Write a program that stores your name, age, and city in variables and displays them.

**Exercise 2: Temperature Conversion**

Write a program that converts a temperature from Celsius to Fahrenheit using the formula:

`Fahrenheit = (Celsius × 9/5) + 32`

**Exercise 3: Positive, Negative, or Zero**

Write a program that checks whether a number is positive, negative, or zero.

**Exercise 4: Multiplication Table**

Use a `for` loop to display the multiplication table of a number from 1 to 10.

**Exercise 5: Server Health Check**

Create a variable named `service_status`. Display `"Service is running"` when its value is `"active"`; otherwise, display `"Service requires attention"`.

## 8. What Comes Next?

You now understand the purpose of programming and have explored examples of variables, decisions, loops, calculations, user input, and functions.

**Next lesson: Python Syntax — Learn the Rules for Writing Python Code.**
