# Python Sets
## Work with Unique Collections

### 1. What Are Sets?

A **set** is a Python data structure that stores unique elements. If you add duplicate values, Python keeps only one occurrence of each value.

Think of a set as a collection where every item must be unique.

**Real-world examples:**

- Guest lists: each person appears only once.
- Unique usernames: prevent duplicate names in a collection.
- Product categories: store distinct categories.
- Log analysis: identify unique IP addresses or error codes.
- Data processing: remove duplicate records or values.

Example:

```python
numbers = {1, 2, 3, 2, 4, 3, 5}

print(numbers)
```

**Output:** The set contains only the unique numbers. Their displayed order may vary.

```text
{1, 2, 3, 4, 5}
```

The duplicate values `2` and `3` are automatically eliminated.

**Important characteristics of sets:**

1. Every element is unique.
2. Sets are unordered collections.
3. Sets are mutable, so you can add or remove elements.
4. Sets do not support indexing or slicing.
5. Elements must be hashable, such as strings, integers, and many tuples.
6. Sets can contain elements of different data types.

### 2. Creating Sets

Python provides two common ways to create sets: using curly braces `{}` with values or using the `set()` function.

#### Creating a set with curly braces

```python
numbers = {10, 20, 30, 40, 50}

print(numbers)
print(type(numbers))
```

**Output:**

```text
{10, 20, 30, 40, 50}
<class 'set'>
```

#### Creating a set using `set()`

```python
fruits = set(["apple", "banana", "orange"])

print(fruits)
```

**Output:** The set contains `"apple"`, `"banana"`, and `"orange"`. The displayed order may vary.

```text
{'apple', 'banana', 'orange'}
```

#### Creating an empty set

This is an important Python concept.

```python
empty_set = set()

print(empty_set)
print(type(empty_set))
```

**Output:**

```text
set()
<class 'set'>
```

Do not use `{}` to create an empty set.

```python
data = {}

print(type(data))
```

**Output:**

```text
<class 'dict'>
```

Empty curly braces create a dictionary, not a set.

**Remember:**

- `{1, 2, 3}` creates a set.
- `set()` creates an empty set.
- `{}` creates an empty dictionary.

#### Creating a set from a list

Sets are especially useful for removing duplicate values.

```python
scores = [85, 90, 85, 92, 90, 95]

unique_scores = set(scores)

print(unique_scores)
```

**Output:** The set contains `85`, `90`, `92`, and `95`. Their displayed order may vary.

```text
{85, 90, 92, 95}
```

Python automatically removes duplicates when constructing the set.

### 3. Adding Elements to Sets

You can add new elements to an existing set using `add()`.

```python
colors = {"red", "blue"}

colors.add("green")

print(colors)
```

**Output:** The set contains `"red"`, `"blue"`, and `"green"`. The displayed order may vary.

```text
{'red', 'blue', 'green'}
```

If the element already exists, adding it again does not create a duplicate.

```python
numbers = {10, 20, 30}

numbers.add(20)

print(numbers)
```

**Output:**

```text
{10, 20, 30}
```

The set remains unchanged because `20` already exists.

#### Adding multiple elements with `update()`

Use `update()` to add multiple elements from an iterable, such as a list, tuple, or another set.

```python
colors = {"red", "blue"}

colors.update(["green", "yellow", "black"])

print(colors)
```

**Output:** The set contains all five unique colors. The displayed order may vary.

```text
{'red', 'blue', 'green', 'yellow', 'black'}
```

### 4. Removing Elements from Sets

Python provides several methods to remove elements.

#### Using `remove()`

Removes the specified element. If the element does not exist, Python raises a `KeyError`.

```python
colors = {"red", "blue", "green"}

colors.remove("blue")

print(colors)
```

**Output:** The set contains `"red"` and `"green"`.

```text
{'red', 'green'}
```

#### Using `discard()`

Removes the element if it exists. If it does not exist, Python does not raise an error.

```python
colors = {"red", "blue", "green"}

colors.discard("yellow")

print(colors)
```

**Output:** The set remains unchanged.

```text
{'red', 'blue', 'green'}
```

Use `discard()` when you are unsure whether an element is present.

#### Using `pop()`

Removes and returns an arbitrary element from the set. Because sets are unordered, you should not expect a particular element to be removed.

```python
numbers = {10, 20, 30}

removed = numbers.pop()

print("Removed:", removed)
print("Remaining:", numbers)
```

**Output:** The exact removed element and remaining set can vary.

For example:

```text
Removed: 10
Remaining: {20, 30}
```

#### Using `clear()`

Removes all elements from the set.

```python
numbers = {10, 20, 30}

numbers.clear()

print(numbers)
```

**Output:**

```text
set()
```

### 5. Checking Whether an Element Exists

Use the `in` and `not in` operators to check whether a value is present.

```python
allowed_users = {"alice", "bob", "charlie"}

if "alice" in allowed_users:
    print("Access granted")

if "david" not in allowed_users:
    print("User not found")
```

**Output:**

```text
Access granted
User not found
```

Sets are generally very efficient for membership checks, especially when working with large collections.

#### Practical example: User access validation

```python
allowed_users = {"alice", "bob", "charlie"}

username = "alice"

if username in allowed_users:
    print("Welcome!")
else:
    print("Access denied.")
```

**Output:**

```text
Welcome!
```

This demonstrates a simple allowlist check. In a real application, authorization should also account for authentication, permissions, and other security requirements.

### 6. Removing Duplicates from a List

One of the most common uses of sets is eliminating duplicates.

```python
names = ["Alice", "Bob", "Alice", "Charlie", "Bob"]

unique_names = set(names)

print(unique_names)
```

**Output:** The set contains `"Alice"`, `"Bob"`, and `"Charlie"`, in no guaranteed display order.

```text
{'Alice', 'Bob', 'Charlie'}
```

If you need the result as a list, convert the set back into a list.

```python
names = ["Alice", "Bob", "Alice", "Charlie", "Bob"]

unique_names = list(set(names))

print(unique_names)
```

The result contains each name once, but the order may differ from the original list.

#### What if the original order matters?

A set does not preserve the original sequence order. If you want to remove duplicates while retaining the first occurrence of each item, use `dict.fromkeys()`:

```python
names = ["Alice", "Bob", "Alice", "Charlie", "Bob"]

unique_names = list(dict.fromkeys(names))

print(unique_names)
```

**Output:**

```text
['Alice', 'Bob', 'Charlie']
```

This technique works for hashable elements such as strings and numbers.

### 7. Set Operations

Sets are particularly powerful because they support mathematical set operations. These operations help compare collections and identify shared or different elements.

Consider two sets:

```python
devops_tools = {"Docker", "Kubernetes", "Jenkins", "Terraform"}

cloud_tools = {"AWS", "Azure", "Docker", "Terraform"}
```

#### Union — Combine elements from both sets

The union operator `|` combines elements from both sets, without duplicates.

```python
print(devops_tools | cloud_tools)
```

**Output:** All seven unique tools appear, in no guaranteed display order.

```text
{'Docker', 'Kubernetes', 'Jenkins', 'Terraform', 'AWS', 'Azure'}
```

#### Intersection — Find common elements

The intersection operator `&` returns elements present in both sets.

```python
print(devops_tools & cloud_tools)
```

**Output:**

```text
{'Docker', 'Terraform'}
```

Both collections contain Docker and Terraform.

#### Difference — Find elements in one set but not the other

The difference operator `-` returns elements that belong to the left-hand set but not the right-hand set.

```python
print(devops_tools - cloud_tools)
```

**Output:** The result contains `"Kubernetes"` and `"Jenkins"`, in no guaranteed display order.

```text
{'Kubernetes', 'Jenkins'}
```

Reverse the order to find tools in `cloud_tools` that are not in `devops_tools`.

```python
print(cloud_tools - devops_tools)
```

**Output:** The result contains `"AWS"` and `"Azure"`.

```text
{'AWS', 'Azure'}
```

#### Symmetric difference — Find elements that are not shared

The symmetric difference operator `^` returns elements found in either set, but not in both.

```python
print(devops_tools ^ cloud_tools)
```

**Output:** The result contains `"Kubernetes"`, `"Jenkins"`, `"AWS"`, and `"Azure"`, in no guaranteed display order.

```text
{'Kubernetes', 'Jenkins', 'AWS', 'Azure'}
```

#### Summary of set operations

| Operation | Operator | Meaning |
|---|---|---|
| Union | `A \| B` | All unique elements from both sets |
| Intersection | `A & B` | Elements common to both sets |
| Difference | `A - B` | Elements in A but not B |
| Symmetric difference | `A ^ B` | Elements in either set, but not both |

These operations are useful for comparing users, software packages, server inventories, cloud resources, and monitoring results.

### 8. Useful Set Methods

You can also perform set operations using methods.

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a.union(b))
print(a.intersection(b))
print(a.difference(b))
print(a.symmetric_difference(b))
```

**Output:** The displayed order may vary.

```text
{1, 2, 3, 4, 5}
{3}
{1, 2}
{1, 2, 4, 5}
```

Other useful methods include:

```python
a = {1, 2, 3}

print(a.issubset({1, 2, 3, 4}))
print(a.issuperset({1, 2}))
print(a.isdisjoint({4, 5}))
```

**Output:**

```text
True
True
True
```

- `issubset()` checks whether every element of one set exists in another.
- `issuperset()` checks whether one set contains every element of another.
- `isdisjoint()` checks whether two sets have no common elements.

### 9. Looping Through Sets

You can use a `for` loop to process each element in a set.

```python
services = {"nginx", "mysql", "redis"}

for service in services:
    print(service)
```

**Output:** All three services are printed, but their order may vary.

```text
nginx
redis
mysql
```

Do not rely on a particular iteration order. If you need predictable output, sort the values first.

```python
services = {"nginx", "mysql", "redis"}

for service in sorted(services):
    print(service)
```

**Output:**

```text
mysql
nginx
redis
```

The `sorted()` function returns a sorted list; it does not change the original set.

### 10. Common Mistakes

#### Mistake 1: Creating an empty set incorrectly

Incorrect:

```python
data = {}

print(type(data))
```

Output:

```text
<class 'dict'>
```

Correct:

```python
data = set()

print(type(data))
```

Output:

```text
<class 'set'>
```

#### Mistake 2: Expecting duplicates to remain

```python
numbers = {10, 10, 20, 20, 30}

print(len(numbers))
```

Output:

```text
3
```

A set stores only unique elements.

#### Mistake 3: Trying to access elements by index

Incorrect:

```python
numbers = {10, 20, 30}

print(numbers[0])
```

This raises a `TypeError` because sets do not support indexing.

If you need indexed access, use a list or convert the set to a list. However, converting a set to a list does not restore any original ordering.

#### Mistake 4: Assuming `remove()` never fails

Incorrect:

```python
numbers = {10, 20, 30}

numbers.remove(100)
```

This raises a `KeyError` because `100` is not in the set.

Safer alternative:

```python
numbers.discard(100)

print(numbers)
```

The set remains unchanged.

#### Mistake 5: Adding mutable objects

Lists and dictionaries cannot be elements of a set because they are unhashable.

Incorrect:

```python
data = {[1, 2], [3, 4]}
```

Use immutable, hashable values instead:

```python
data = {(1, 2), (3, 4)}

print(data)
```

**Output:**

```text
{(1, 2), (3, 4)}
```

Tuples are valid set elements when all their contents are hashable.

### 11. Practice Exercises

Try these exercises before checking the sample solutions.

**Exercise 1: Create a set**

Create a set containing the numbers `10`, `20`, `30`, `40`, and `50`. Print the set and its length.

**Exercise 2: Remove duplicates**

Given the following list, create a set containing only unique values.

```python
numbers = [1, 2, 3, 2, 4, 1, 5, 3]
```

**Exercise 3: Add and remove elements**

Create a set containing `"Linux"` and `"Docker"`. Add `"Kubernetes"` and remove `"Docker"`.

**Exercise 4: Check membership**

Create a set of allowed usernames containing `"alice"`, `"bob"`, and `"charlie"`. Check whether `"bob"` is allowed.

**Exercise 5: Set operations**

Given:

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
```

Find the union, intersection, difference (`a - b`), and symmetric difference.

**Exercise 6: DevOps practical exercise**

You have two lists of servers:

```python
production_servers = ["web01", "web02", "db01", "web01"]
monitoring_servers = ["web02", "db01", "monitor01"]
```

Convert the lists to sets and identify:

- All unique servers.
- Servers common to both environments.
- Servers present in production but not in monitoring.

### 12. Sample Solutions

**Solution 1**

```python
numbers = {10, 20, 30, 40, 50}

print(numbers)
print(len(numbers))
```

Output:

```text
{10, 20, 30, 40, 50}
5
```

**Solution 2**

```python
numbers = [1, 2, 3, 2, 4, 1, 5, 3]

unique_numbers = set(numbers)

print(unique_numbers)
```

Output: The set contains `1`, `2`, `3`, `4`, and `5`, in no guaranteed display order.

**Solution 3**

```python
tools = {"Linux", "Docker"}

tools.add("Kubernetes")
tools.remove("Docker")

print(tools)
```

Output:

```text
{'Linux', 'Kubernetes'}
```

**Solution 4**

```python
allowed_users = {"alice", "bob", "charlie"}

if "bob" in allowed_users:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

**Solution 5**

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print("Union:", a | b)
print("Intersection:", a & b)
print("Difference:", a - b)
print("Symmetric difference:", a ^ b)
```

Output, with set elements shown in one possible order:

```text
Union: {1, 2, 3, 4, 5, 6}
Intersection: {3, 4}
Difference: {1, 2}
Symmetric difference: {1, 2, 5, 6}
```

**Solution 6**

```python
production_servers = ["web01", "web02", "db01", "web01"]
monitoring_servers = ["web02", "db01", "monitor01"]

production = set(production_servers)
monitoring = set(monitoring_servers)

print("All unique servers:", production | monitoring)
print("Common servers:", production & monitoring)
print("Production only:", production - monitoring)
```

Output, with set elements shown in one possible order:

```text
All unique servers: {'web01', 'web02', 'db01', 'monitor01'}
Common servers: {'web02', 'db01'}
Production only: {'web01'}
```

### 13. Quick Summary

| Concept | Example | Purpose |
|---|---|---|
| Create a set | `{1, 2, 3}` | Store unique elements |
| Empty set | `set()` | Create an empty set |
| Add one element | `s.add(10)` | Add an element |
| Add multiple elements | `s.update([10, 20])` | Add elements from an iterable |
| Remove an element | `s.remove(10)` | Remove an existing element |
| Remove safely | `s.discard(10)` | Remove without an error if absent |
| Check membership | `10 in s` | Check whether an element exists |
| Remove duplicates | `set(my_list)` | Keep only unique values |
| Union | `a \| b` | Combine unique elements |
| Intersection | `a & b` | Find common elements |
| Difference | `a - b` | Find elements in A but not B |
| Symmetric difference | `a ^ b` | Find elements that are not shared |

**Key takeaway:** Use sets when uniqueness matters, when you need efficient membership checks, or when you want to compare collections using union, intersection, and difference.

### Congratulations! You've Completed Python Basics

You have now learned the four major Python collection types:

| Data structure | Ordered? | Mutable? | Allows duplicates? |
|---|---|---|---|
| List | Yes | Yes | Yes |
| Tuple | Yes | No | Yes |
| Dictionary | Yes (insertion order) | Yes | Keys must be unique |
| Set | No guaranteed order | Yes | No |

The next step is to combine these fundamentals to build real Python programs using variables, data types, conditions, loops, functions, and collections.

**Recommended next lesson: Python Functions — Organize Code into Reusable Blocks.**
