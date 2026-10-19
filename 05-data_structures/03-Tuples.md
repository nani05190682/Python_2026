# Python Tuples
## Work with Immutable Sequences

### 1. What Are Tuples?

A **tuple** is a Python data structure that stores multiple items in a single variable. Tuples are similar to lists, but the main difference is that **tuples are immutable**, meaning you cannot change their elements after creating them.

Think of a tuple as a container whose contents cannot be reassigned, added to, or removed from after creation.

**Real-world examples:**

- Coordinates: `(10, 20)`
- RGB colors: `(255, 0, 0)`
- Database records: `("Ravi", 35, "DevOps")`
- Days of the week: `("Monday", "Tuesday", "Wednesday")`
- Function return values: `(status, message)`

Example:

```python
point = (3, 5)

print(point)
print(type(point))
```

**Output:**

```text
(3, 5)
<class 'tuple'>
```

Here, `point` stores two values: `3` and `5`.

### 2. Creating Tuples

Tuples are usually created using parentheses `()` with items separated by commas.

#### Creating an empty tuple

```python
empty = ()

print(empty)
print(type(empty))
```

**Output:**

```text
()
<class 'tuple'>
```

#### Creating a tuple with multiple items

```python
colors = ("red", "green", "blue")

print(colors)
```

**Output:**

```text
('red', 'green', 'blue')
```

#### Creating a tuple with different data types

A tuple can contain values of different data types.

```python
employee = ("Ravi", 35, 75000.50, True)

print(employee)
```

**Output:**

```text
('Ravi', 35, 75000.5, True)
```

The tuple contains a string, an integer, a float, and a Boolean.

#### Creating a single-item tuple

This is an important Python concept.

```python
single = (42,)

print(single)
print(type(single))
```

**Output:**

```text
(42,)
<class 'tuple'>
```

Notice the comma after `42`. The comma makes this a tuple.

Without the comma:

```python
number = (42)

print(number)
print(type(number))
```

**Output:**

```text
42
<class 'int'>
```

Python treats `(42)` as an integer inside parentheses, not as a tuple.

**Remember:** A single-item tuple requires a comma: `(42,)`.

#### Creating a tuple without parentheses

Python also allows you to create tuples by separating values with commas.

```python
coordinates = 10, 20

print(coordinates)
print(type(coordinates))
```

**Output:**

```text
(10, 20)
<class 'tuple'>
```

The commas define the tuple; parentheses are often used for clarity.

### 3. Accessing Tuple Items

Tuples use indexing, just like lists. Python indexing starts at `0`.

```python
colors = ("red", "green", "blue")

print(colors[0])
print(colors[1])
print(colors[2])
```

**Output:**

```text
red
green
blue
```

#### Negative indexing

Negative indexes count from the end of the tuple.

```python
colors = ("red", "green", "blue")

print(colors[-1])
print(colors[-2])
print(colors[-3])
```

**Output:**

```text
blue
green
red
```

- `-1` refers to the last item.
- `-2` refers to the second-to-last item.
- `-3` refers to the third-to-last item.

### 4. Slicing Tuples

Slicing lets you retrieve a portion of a tuple.

The syntax is:

```python
tuple_name[start:stop:step]
```

The `stop` index is excluded.

Example:

```python
colors = ("red", "green", "blue", "yellow")

print(colors[0:2])
print(colors[1:3])
print(colors[:3])
print(colors[2:])
```

**Output:**

```text
('red', 'green')
('green', 'blue')
('red', 'green', 'blue')
('blue', 'yellow')
```

You can also use a step:

```python
numbers = (10, 20, 30, 40, 50, 60)

print(numbers[::2])
```

**Output:**

```text
(10, 30, 50)
```

The `::2` slice selects every second item.

### 5. Tuples Are Immutable

The most important characteristic of tuples is immutability.

Once a tuple is created, you cannot change an individual element.

Incorrect example:

```python
colors = ("red", "green", "blue")

colors[0] = "yellow"
```

**Output:**

```text
TypeError: 'tuple' object does not support item assignment
```

Python raises a `TypeError` because tuples do not support item assignment.

You also cannot add or remove individual elements using list methods such as `append()` or `remove()`.

```python
numbers = (10, 20, 30)

numbers.append(40)
```

This raises an `AttributeError` because tuples do not have an `append()` method.

#### How can you change tuple data?

If you need different contents, create a new tuple or convert the tuple into a list, modify the list, and convert it back.

```python
colors = ("red", "green", "blue")

color_list = list(colors)
color_list[0] = "yellow"

colors = tuple(color_list)

print(colors)
```

**Output:**

```text
('yellow', 'green', 'blue')
```

This does not modify the original tuple in place. It creates a list, changes that list, and assigns a newly created tuple to `colors`.

### 6. Tuple Unpacking

**Tuple unpacking** means assigning the elements of a tuple to separate variables.

This is one of Python's most useful tuple features.

```python
point = (3, 5)

x, y = point

print(x)
print(y)
```

**Output:**

```text
3
5
```

Python assigns the first element to `x` and the second element to `y`.

#### Unpacking multiple values

```python
employee = ("Ravi", 35, "DevOps")

name, age, department = employee

print(name)
print(age)
print(department)
```

**Output:**

```text
Ravi
35
DevOps
```

The number of variables on the left must match the number of values being unpacked, unless you use extended unpacking with `*`.

For example, this raises a `ValueError`:

```python
point = (3, 5)

x = point
a, b, c = point
```

The tuple contains two elements, but three variables are requested in the second assignment.

#### Multiple assignment

You can assign several variables in one statement.

```python
a, b, c = 10, 20, 30

print(a)
print(b)
print(c)
```

**Output:**

```text
10
20
30
```

This is often called iterable unpacking. The values on the right are packed into a tuple-like sequence for the assignment.

#### Swapping variables

Python allows you to swap values without using a temporary variable.

```python
x = 10
y = 20

x, y = y, x

print(x)
print(y)
```

**Output:**

```text
20
10
```

Python evaluates the right-hand side first and then assigns the values to the variables on the left.

### 7. Useful Tuple Operations and Methods

Although tuples are immutable, you can still search, count, and retrieve information from them.

#### `len()` — Count items

```python
numbers = (10, 20, 30, 40)

print(len(numbers))
```

**Output:**

```text
4
```

#### `count()` — Count occurrences

```python
numbers = (10, 20, 10, 30, 10)

print(numbers.count(10))
print(numbers.count(20))
```

**Output:**

```text
3
1
```

The `count()` method returns how many times a value appears.

#### `index()` — Find an item's position

```python
colors = ("red", "green", "blue")

print(colors.index("green"))
```

**Output:**

```text
1
```

The `index()` method returns the position of the first matching item. If the value is not present, Python raises a `ValueError`.

#### Membership testing

Use `in` or `not in` to check whether an item exists.

```python
servers = ("web01", "db01", "app01")

print("db01" in servers)
print("mail01" not in servers)
```

**Output:**

```text
True
True
```

#### Concatenation

You can combine tuples using `+`. This creates a new tuple.

```python
first = (10, 20)
second = (30, 40)

combined = first + second

print(combined)
```

**Output:**

```text
(10, 20, 30, 40)
```

#### Repetition

The `*` operator repeats the tuple's elements.

```python
numbers = (1, 2)

print(numbers * 3)
```

**Output:**

```text
(1, 2, 1, 2, 1, 2)
```

### 8. Looping Through Tuples

You can use a `for` loop to process each item.

```python
servers = ("web01", "db01", "app01")

for server in servers:
    print(server)
```

**Output:**

```text
web01
db01
app01
```

You can also use `enumerate()` when you need both the index and the value.

```python
servers = ("web01", "db01", "app01")

for index, server in enumerate(servers):
    print(f"{index}: {server}")
```

**Output:**

```text
0: web01
1: db01
2: app01
```

This is useful when you need to display an ordered sequence with its positions.

### 9. Tuples Inside Other Data Structures

Tuples can be stored inside lists and dictionaries. This is useful when you want to represent records or fixed groups of values.

#### List of tuples

```python
employees = [
    ("Ravi", "DevOps"),
    ("Priya", "Development"),
    ("Arun", "Testing")
]

for name, department in employees:
    print(f"{name} works in {department}")
```

**Output:**

```text
Ravi works in DevOps
Priya works in Development
Arun works in Testing
```

Each tuple represents one employee record.

#### Tuples as dictionary keys

Tuples can be dictionary keys when all their elements are hashable.

```python
locations = {
    (12.97, 77.59): "Bengaluru",
    (13.08, 80.27): "Chennai"
}

print(locations[(12.97, 77.59)])
```

**Output:**

```text
Bengaluru
```

This is useful for representing fixed coordinate pairs or other compound keys.

### 10. Tuple vs. List

Both tuples and lists store ordered sequences, but they have important differences.

| Feature | List | Tuple |
|---|---|---|
| Syntax | `[10, 20, 30]` | `(10, 20, 30)` |
| Mutable? | Yes | No |
| Can change an element? | Yes | No |
| Can append or remove items? | Yes | No |
| Indexing and slicing | Supported | Supported |
| Allows duplicate values? | Yes | Yes |
| Can be a dictionary key? | No | Yes, if all elements are hashable |
| Common use | Data that changes | Data that should remain fixed |

#### When should you use a tuple?

Use a tuple when:

- You are representing a fixed group of related values.
- You want to prevent accidental reassignment of tuple elements.
- You need a hashable compound key, such as a coordinate pair.
- A function needs to return multiple values.

Use a list when you need to add, remove, or update individual elements.

**Important:** A tuple is immutable, but if it contains a mutable object such as a list, that nested object may still be changed.

Example:

```python
data = (10, [20, 30])

data[1].append(40)

print(data)
```

**Output:**

```text
(10, [20, 30, 40])
```

The tuple's second element still refers to the same list, and that list can be modified. Immutability prevents reassignment of the tuple's elements; it does not automatically make nested objects immutable.

### 11. Common Mistakes

**Mistake 1: Forgetting the comma in a single-item tuple**

Incorrect:

```python
item = (42)

print(type(item))
```

Output:

```text
<class 'int'>
```

Correct:

```python
item = (42,)

print(type(item))
```

Output:

```text
<class 'tuple'>
```

**Mistake 2: Trying to modify a tuple**

Incorrect:

```python
numbers = (10, 20, 30)

numbers[0] = 100
```

This raises `TypeError`.

Correct approach when a modified sequence is required:

```python
numbers = (10, 20, 30)

updated = (100,) + numbers[1:]

print(updated)
```

Output:

```text
(100, 20, 30)
```

This creates a new tuple rather than changing the existing tuple in place.

**Mistake 3: Unpacking the wrong number of values**

Incorrect:

```python
point = (10, 20)

x, y, z = point
```

This raises `ValueError` because there are two values but three variables.

Correct:

```python
x, y = point
```

**Mistake 4: Using list methods on tuples**

Incorrect:

```python
numbers = (1, 2, 3)

numbers.append(4)
```

Tuples do not have an `append()` method. Convert the tuple to a list if you need to add items, then create a new tuple if necessary.

### 12. Practice Exercises

Try these exercises yourself before checking the solutions.

**Exercise 1: Create a tuple**

Create a tuple called `fruits` containing `"apple"`, `"banana"`, and `"orange"`. Print the first and last items.

**Exercise 2: Single-item tuple**

Create a tuple containing only the number `100`. Print its type.

**Exercise 3: Tuple slicing**

Given the tuple below, print the first three elements.

```python
numbers = (10, 20, 30, 40, 50)
```

**Exercise 4: Tuple unpacking**

Create a tuple containing a server's hostname, IP address, and status. Unpack the values into three variables and print each variable.

**Exercise 5: Count occurrences**

Given the following tuple, count how many times the number `5` appears.

```python
numbers = (5, 10, 5, 15, 5, 20)
```

**Exercise 6: Swap variables**

Create two variables, `a = 100` and `b = 200`. Swap their values using Python's multiple assignment syntax.

**Exercise 7: Practical DevOps example**

Create a tuple containing the names of three services: `nginx`, `mysql`, and `redis`. Loop through the tuple and print each service name.

### 13. Sample Solutions

**Solution 1**

```python
fruits = ("apple", "banana", "orange")

print(fruits[0])
print(fruits[-1])
```

Output:

```text
apple
orange
```

**Solution 2**

```python
value = (100,)

print(type(value))
```

Output:

```text
<class 'tuple'>
```

**Solution 3**

```python
numbers = (10, 20, 30, 40, 50)

print(numbers[:3])
```

Output:

```text
(10, 20, 30)
```

**Solution 4**

```python
server = ("web01", "192.168.1.10", "running")

hostname, ip_address, status = server

print(hostname)
print(ip_address)
print(status)
```

Output:

```text
web01
192.168.1.10
running
```

**Solution 5**

```python
numbers = (5, 10, 5, 15, 5, 20)

print(numbers.count(5))
```

Output:

```text
3
```

**Solution 6**

```python
a = 100
b = 200

a, b = b, a

print(a)
print(b)
```

Output:

```text
200
100
```

**Solution 7**

```python
services = ("nginx", "mysql", "redis")

for service in services:
    print(service)
```

Output:

```text
nginx
mysql
redis
```

### 14. Quick Summary

| Concept | Example | Purpose |
|---|---|---|
| Create a tuple | `t = (10, 20)` | Store an ordered sequence |
| Single-item tuple | `t = (10,)` | Create a tuple with one item |
| Access an item | `t[0]` | Retrieve an element |
| Slice a tuple | `t[:2]` | Retrieve part of a tuple |
| Unpack a tuple | `x, y = (10, 20)` | Assign elements to variables |
| Count an item | `t.count(10)` | Count occurrences |
| Find an index | `t.index(20)` | Find the first matching position |
| Check membership | `10 in t` | Check whether an item exists |
| Get the length | `len(t)` | Count the elements |
| Concatenate tuples | `t1 + t2` | Create a combined tuple |

**Key takeaway:** Tuples are ordered, immutable sequences. They are useful when you need to group related values and do not want to reassign the sequence's elements.

### What's Next?

**Python Sets — Work with Collections of Unique Items**

Next, you'll learn how sets automatically eliminate duplicate values, how to add and remove elements, and how to perform union, intersection, and difference operations.
