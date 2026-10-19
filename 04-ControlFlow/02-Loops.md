# Loops in Python
## Repeat Code Multiple Times

### 1. What Are Loops?

Loops allow you to execute a block of code repeatedly without writing the same instructions multiple times.

Imagine you want to print `"Hello!"` five times.

Without a loop:

```python
print("Hello!")
print("Hello!")
print("Hello!")
print("Hello!")
print("Hello!")
```

With a loop:

```python
for i in range(5):
    print("Hello!")
```

Both programs produce the same output, but the loop is shorter, cleaner, and easier to maintain.

Loops are especially useful when you need to:
- Process hundreds of files.
- Check the status of multiple servers.
- Read records from a database.
- Process log entries.
- Repeat a task until a condition is satisfied.

Python provides two main types of loops:

- **`for` loops** — iterate over a sequence or other iterable, such as a string, list, or range of numbers.
- **`while` loops** — repeat a block of code while a condition remains true.

Let's explore both.

### 2. For Loops

A `for` loop repeats a block of code for each item in an iterable.

Basic syntax:

```python
for variable in iterable:
    # Code to execute during each iteration
```

Here:
- `for` starts the loop.
- `variable` holds the current item.
- `in` specifies the iterable to process.
- The colon (`:`) marks the beginning of the loop body.
- Indented statements execute during each iteration.

### 3. Repeating Code a Specific Number of Times

Python's `range()` function is commonly used when you want to repeat code a specific number of times.

Example:

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

The loop executes five times.

Why does it start at `0`?

`range(5)` generates the numbers `0`, `1`, `2`, `3`, and `4`. The stopping value `5` is excluded.

This behavior is common in Python and is important to understand when working with loops and indexes.

#### Counting from 1 to 5

```python
for i in range(1, 6):
    print(i)
```

Output:

```text
1
2
3
4
5
```

The syntax `range(start, stop)` includes the starting value but excludes the stopping value.

#### Counting in steps

You can also specify a step value.

```python
for i in range(0, 10, 2):
    print(i)
```

Output:

```text
0
2
4
6
8
```

Here, `range(0, 10, 2)` starts at `0`, increases by `2`, and stops before `10`.

The general syntax is:

```python
range(start, stop, step)
```

You can count backward by using a negative step.

```python
for i in range(5, 0, -1):
    print(i)
```

Output:

```text
5
4
3
2
1
```

This is useful for countdowns and other tasks that require descending numbers.

### 4. Looping Through Strings

A string is a sequence of characters. You can use a `for` loop to process each character individually.

Example:

```python
name = "Python"

for letter in name:
    print(letter)
```

Output:

```text
P
y
t
h
o
n
```

During each iteration, the variable `letter` holds the next character in the string.

You can also perform an operation on each character.

```python
name = "Python"

for letter in name:
    print(f"Character: {letter}")
```

Output:

```text
Character: P
Character: y
Character: t
Character: h
Character: o
Character: n
```

### 5. Looping Through Lists

A list stores multiple values in a single variable. You can use a `for` loop to process each item.

Example:

```python
colors = ["red", "blue", "green"]

for color in colors:
    print(f"I like {color}")
```

Output:

```text
I like red
I like blue
I like green
```

Here, `color` holds one item from the list during each iteration.

This approach is useful when working with multiple servers, files, usernames, or configuration values.

For example:

```python
servers = ["web-01", "web-02", "db-01"]

for server in servers:
    print(f"Checking server: {server}")
```

Output:

```text
Checking server: web-01
Checking server: web-02
Checking server: db-01
```

This example prints each server name. A real monitoring program would need additional code to check the actual health of each server.

### 6. While Loops

A `while` loop repeatedly executes a block of code as long as its condition is true.

Basic syntax:

```python
while condition:
    # Code to execute repeatedly
```

Example:

```python
count = 0

while count < 5:
    print(f"Count is {count}")
    count = count + 1
```

Output:

```text
Count is 0
Count is 1
Count is 2
Count is 3
Count is 4
```

#### How it works

1. Python initializes `count` to `0`.
2. It checks whether `count < 5`.
3. If the condition is true, it prints the current value.
4. It increases `count` by `1`.
5. It checks the condition again.
6. When `count` becomes `5`, the condition is false, so the loop stops.

You can write `count = count + 1` more concisely as `count += 1`.

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

Both versions produce the same output.

### 7. The Difference Between For and While Loops

| Feature | `for` loop | `while` loop |
|---|---|---|
| Best suited for | Iterating over items or a known range | Repeating while a condition is true |
| Typical use | Processing a list of servers | Waiting for a condition to change |
| Loop control | Advances through the iterable | Depends on the condition |
| Common risk | Incorrect range boundaries | Infinite loops if the condition never becomes false |

Use a `for` loop when you want to process a known sequence of items.

Use a `while` loop when the number of iterations depends on a condition.

### 8. Avoiding Infinite Loops

An infinite loop occurs when a loop never reaches a stopping condition.

Consider this example:

```python
count = 0

while count < 5:
    print(count)
```

The variable `count` never changes. Therefore, `count < 5` remains true, and the loop continues indefinitely.

Correct version:

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

Now the loop eventually stops because `count` increases during every iteration.

**Important:** Always check that a `while` loop has a clear path to termination, unless you deliberately want a continuously running process.

### 9. Loop Control Statements

Python provides statements that change the normal behavior of a loop.

#### A. The `break` statement

`break` immediately exits the nearest enclosing loop.

```python
for number in range(1, 10):
    if number == 5:
        break

    print(number)
```

Output:

```text
1
2
3
4
```

When `number` reaches `5`, the loop terminates.

#### B. The `continue` statement

`continue` skips the remaining statements in the current iteration and proceeds to the next iteration.

```python
for number in range(1, 6):
    if number == 3:
        continue

    print(number)
```

Output:

```text
1
2
4
5
```

The number `3` is skipped, but the loop continues.

#### C. The `pass` statement

`pass` is a placeholder statement that performs no action.

```python
for number in range(3):
    pass

print("Loop completed.")
```

Output:

```text
Loop completed.
```

It is useful when you need to write the structure of a loop before implementing its logic.

### 10. Common Mistakes to Avoid

**Mistake 1: Forgetting the colon**

Incorrect:

```python
# for i in range(5)
#     print(i)
```

This causes a `SyntaxError` because the loop header is missing a colon.

Correct:

```python
for i in range(5):
    print(i)
```

**Mistake 2: Incorrect indentation**

Incorrect:

```python
# for i in range(5):
# print(i)
```

The statement inside the loop must be indented.

Correct:

```python
for i in range(5):
    print(i)
```

**Mistake 3: Off-by-one errors**

Consider:

```python
for i in range(1, 5):
    print(i)
```

Output:

```text
1
2
3
4
```

The loop does not print `5` because the stopping value is excluded.

To print numbers from `1` to `5`, use:

```python
for i in range(1, 6):
    print(i)
```

**Mistake 4: Forgetting to update a while-loop variable**

If a loop condition depends on a variable, make sure the loop body changes that variable when necessary. Otherwise, the loop might never terminate.

### 11. Practice Exercises

Create a file named `loops_practice.py` and complete the following tasks.

**Task 1: Print numbers**

Use a `for` loop to print numbers from `1` to `10`.

**Task 2: Print even numbers**

Use `range()` to print all even numbers from `2` to `20`.

**Task 3: Repeat a message**

Ask the user to enter a message and the number of times to repeat it. Use a loop to print the message the requested number of times.

**Task 4: Calculate a total**

Given the following list, calculate the total using a `for` loop.

```python
numbers = [10, 20, 30, 40, 50]
```

Expected result:

```text
Total: 150
```

**Task 5: Countdown**

Use a `while` loop to print numbers from `5` down to `1`, followed by `"Blast off!"`.

**Task 6: Process server names**

Given this list, print each server name with a status message.

```python
servers = ["web-01", "web-02", "db-01"]
```

Expected output:

```text
Checking web-01
Checking web-02
Checking db-01
```

### 12. Sample Solution

```python
# Task 1: Print numbers from 1 to 10
for number in range(1, 11):
    print(number)

# Task 2: Print even numbers from 2 to 20
for number in range(2, 21, 2):
    print(number)

# Task 3: Repeat a message
message = input("Enter a message: ")
repetitions = int(input("How many times should it repeat? "))

for _ in range(repetitions):
    print(message)

# Task 4: Calculate a total
numbers = [10, 20, 30, 40, 50]
total = 0

for number in numbers:
    total += number

print("Total:", total)

# Task 5: Countdown
count = 5

while count > 0:
    print(count)
    count -= 1

print("Blast off!")

# Task 6: Process server names
servers = ["web-01", "web-02", "db-01"]

for server in servers:
    print(f"Checking {server}")
```

### 13. Summary

In this lesson, you learned:

- Loops repeat instructions without duplicating code.
- `for` loops iterate over ranges, strings, lists, and other iterables.
- `range()` generates a sequence of numbers.
- `while` loops continue while a condition is true.
- `break` exits a loop.
- `continue` skips to the next iteration.
- `pass` acts as a placeholder.
- Correct indentation, loop boundaries, and termination conditions are essential.

### What's Next?

**Working with Lists in Python**

Learn how to store multiple values, access individual elements, add and remove items, and process collections of data using loops.
