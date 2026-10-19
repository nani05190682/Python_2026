# If Statements in Python
## Make Decisions in Your Code

### 1. What Are If Statements?

An `if` statement allows a Python program to make decisions based on conditions.

A program evaluates a condition. If the condition is `True`, Python executes the code inside the `if` block. If the condition is `False`, Python skips that block.

Think about everyday decisions:

- **Weather:** If it is raining, take an umbrella.
- **Mobile phone:** If the battery is below 20%, charge the phone.
- **Login system:** If the password is correct, allow access.
- **Exam results:** If the score meets the passing mark, declare the student passed.

In programming, these decisions are implemented using conditional statements.

### 2. Basic If Statement

Let's start with a simple example.

```python
age = 18

if age >= 18:
    print("You can vote!")
    print("You are an adult.")
```

Output:

```text
You can vote!
You are an adult.
```

**How it works:**

1. Python checks the condition `age >= 18`.
2. The condition evaluates to `True`.
3. Python executes both indented `print()` statements.

Now change the age to `15`.

```python
age = 15

if age >= 18:
    print("You can vote!")
    print("You are an adult.")
```

Output: No output is displayed because the condition is `False`.

#### Understanding the syntax

```python
if condition:
    # Code executes when the condition is True
```

Three important rules:

- Write the keyword `if` followed by a condition.
- Add a colon (`:`) at the end of the condition.
- Indent the statements inside the `if` block, normally using four spaces.

Python uses indentation to determine which statements belong to the conditional block.

### 3. If-Else Statements

An `if` statement executes code only when its condition is true. What if you want your program to do something when the condition is false?

Use an `if-else` statement.

Example:

```python
temperature = 25

if temperature > 30:
    print("It's hot!")
else:
    print("Nice weather!")
```

Output:

```text
Nice weather!
```

**How it works:**

- If `temperature > 30` is `True`, Python prints `"It's hot!"`.
- Otherwise, Python executes the `else` block and prints `"Nice weather!"`.

Only one of these two blocks executes.

Another example:

```python
score = 45

if score >= 60:
    print("You passed the exam.")
else:
    print("You did not pass the exam.")
```

Output:

```text
You did not pass the exam.
```

Use `if-else` whenever you need to choose between two alternatives.

### 4. If-Elif-Else Statements

Sometimes a program must choose between more than two possibilities.

Python provides `elif`, which means *else if*.

Example: Assigning a grade based on a student's score.

```python
score = 85

if score >= 90:
    print("A - Excellent!")
elif score >= 80:
    print("B - Good job!")
elif score >= 70:
    print("C - Keep it up!")
else:
    print("F - Need improvement.")
```

Output:

```text
B - Good job!
```

#### How it works

1. Python checks whether `score >= 90`. It is false.
2. Python checks whether `score >= 80`. It is true.
3. Python executes the corresponding block.
4. Python skips the remaining conditions.

Only the first matching block executes in an `if-elif-else` chain.

#### Why use `elif` instead of multiple `if` statements?

Consider this example:

```python
score = 95

if score >= 70:
    print("Passed")

if score >= 80:
    print("Good")

if score >= 90:
    print("Excellent")
```

Output:

```text
Passed
Good
Excellent
```

All three conditions are true, so all three blocks execute.

Now use an `if-elif-else` chain:

```python
score = 95

if score >= 90:
    print("Excellent")
elif score >= 80:
    print("Good")
elif score >= 70:
    print("Passed")
else:
    print("Need improvement")
```

Output:

```text
Excellent
```

Only the first matching branch executes.

**Important:** The order of conditions matters. In the grading example, check higher score thresholds first. Otherwise, a score of `95` would match `score >= 70` before reaching the higher grades.

### 5. Combining Multiple Conditions

You can combine conditions using logical operators such as `and`, `or`, and `not`.

#### A. Using `and`

The `and` operator requires both conditions to be true.

```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("You can drive.")
else:
    print("You cannot drive.")
```

Output:

```text
You can drive.
```

Both conditions are true, so the program allows the action under these simplified rules.

#### B. Using `or`

The `or` operator requires at least one condition to be true.

```python
day = "Saturday"
holiday = False

if day == "Saturday" or day == "Sunday" or holiday:
    print("No work today!")
else:
    print("It's a working day.")
```

Output:

```text
No work today!
```

The first condition is true because the day is Saturday.

#### C. Using `not`

The `not` operator reverses a Boolean condition.

```python
raining = False

if not raining:
    print("Let's go outside!")
else:
    print("Take an umbrella.")
```

Output:

```text
Let's go outside!
```

Since `raining` is `False`, `not raining` evaluates to `True`.

### 6. Nested If Statements

A nested `if` statement is an `if` statement placed inside another conditional block.

Nested conditions are useful when one decision depends on another.

Example: Checking movie entry requirements.

```python
has_ticket = True
age = 15

if has_ticket:
    if age >= 18:
        print("Enjoy the movie!")
    else:
        print("Adult supervision is required.")
else:
    print("Please buy a ticket first.")
```

Output:

```text
Adult supervision is required.
```

**How it works:**

1. Python checks `has_ticket`. It is true.
2. Python enters the outer `if` block.
3. Python checks whether `age >= 18`. It is false.
4. Python executes the inner `else` block.

Notice the indentation: the inner `if-else` belongs to the outer `if` block.

### 7. Real-World Example: Server Health Check

Conditional statements are particularly useful in DevOps and SRE automation.

Consider a simple program that checks whether a server is responding.

```python
server_name = "web-server-01"
response_time = 120
server_reachable = True

if not server_reachable:
    print(f"CRITICAL: {server_name} is unreachable.")
elif response_time > 500:
    print(f"WARNING: {server_name} is responding slowly.")
else:
    print(f"OK: {server_name} is healthy.")
```

Output:

```text
OK: web-server-01 is healthy.
```

The program checks conditions in order:

- If the server is unreachable, it reports a critical issue.
- Otherwise, if the response time exceeds 500 milliseconds, it reports a warning.
- Otherwise, it reports the server as healthy.

This is a simplified example. A real monitoring system would collect the reachability and response-time values from actual health checks or monitoring data.

### 8. Common Mistakes to Avoid

#### Mistake 1: Forgetting the colon

Incorrect:

```python
age = 20

# if age >= 18
#     print("You are an adult.")
```

This causes a `SyntaxError` if the code is uncommented because the `if` line is missing a colon.

Correct:

```python
age = 20

if age >= 18:
    print("You are an adult.")
```

#### Mistake 2: Using `=` instead of `==`

Incorrect:

```python
age = 18

# if age = 18:
#     print("Age is 18")
```

Assignment with `=` cannot be used as a condition in an ordinary `if` statement.

Correct:

```python
age = 18

if age == 18:
    print("Age is 18")
```

#### Mistake 3: Incorrect indentation

Incorrect:

```python
age = 20

# if age >= 18:
# print("You are an adult.")
```

Python expects the statement inside the `if` block to be indented.

Correct:

```python
age = 20

if age >= 18:
    print("You are an adult.")
```

#### Mistake 4: Incorrect condition order

Incorrect:

```python
score = 95

if score >= 70:
    print("Passed")
elif score >= 90:
    print("Excellent")
```

Output:

```text
Passed
```

The first condition is already true, so Python never checks the `elif` condition.

Correct:

```python
score = 95

if score >= 90:
    print("Excellent")
elif score >= 70:
    print("Passed")
else:
    print("Need improvement")
```

Output:

```text
Excellent
```

### 9. Practice Exercises

Create a Python file named `if_statements_practice.py` and complete the following tasks.

**Task 1: Check voting eligibility**

Ask the user to enter their age. Print `"You can vote."` if the age is at least 18; otherwise, print `"You cannot vote yet."`

**Task 2: Check whether a number is even or odd**

Ask the user to enter an integer. Use the modulo operator (`%`) to determine whether the number is even or odd.

**Task 3: Assign a grade**

Use the following grading rules:

| Score | Grade |
|---|---|
| 90–100 | A |
| 80–89 | B |
| 70–79 | C |
| 60–69 | D |
| Below 60 | F |

Ask the user to enter a score and print the corresponding grade. Assume the score must be between 0 and 100.

**Task 4: Login validation**

Create two variables:

```python
username = "admin"
password = "python123"
```

Ask the user to enter a username and password. Display `"Login successful"` only when both values match. Otherwise, display `"Invalid username or password"`.

This is a beginner exercise, not a secure authentication implementation. Real applications should never store passwords as plain-text values in source code.

**Task 5: Server status**

Create variables for server reachability and response time. Display:

- `CRITICAL` if the server is unreachable.
- `WARNING` if the server is reachable but its response time exceeds 500 milliseconds.
- `OK` otherwise.

### 10. Sample Solution

```python
# Task 1: Voting eligibility
age = int(input("Enter your age: "))

if age >= 18:
    print("You can vote.")
else:
    print("You cannot vote yet.")

# Task 2: Even or odd
number = int(input("Enter an integer: "))

if number % 2 == 0:
    print("Even number")
else:
    print("Odd number")

# Task 3: Grade assignment
score = int(input("Enter your score (0-100): "))

if score < 0 or score > 100:
    print("Invalid score.")
elif score >= 90:
    print("Grade A")
elif score >= 80:
    print("Grade B")
elif score >= 70:
    print("Grade C")
elif score >= 60:
    print("Grade D")
else:
    print("Grade F")

# Task 4: Login validation
username = "admin"
password = "python123"

entered_username = input("Enter username: ")
entered_password = input("Enter password: ")

if entered_username == username and entered_password == password:
    print("Login successful")
else:
    print("Invalid username or password")

# Task 5: Server status
server_reachable = True
response_time = 650

if not server_reachable:
    print("CRITICAL: Server is unreachable.")
elif response_time > 500:
    print("WARNING: Server is responding slowly.")
else:
    print("OK: Server is healthy.")
```

### 11. Summary

In this lesson, you learned:

- `if` executes code when a condition is true.
- `if-else` chooses between two alternatives.
- `if-elif-else` handles multiple conditions.
- Logical operators combine or reverse conditions.
- Nested `if` statements handle dependent decisions.
- Colons and correct indentation are essential.
- Condition order can change the result of a program.

### What's Next?

**Loops in Python — Repeating Code Efficiently**

Learn how to use `for` and `while` loops to repeat tasks, process lists of data, and automate repetitive operations.
