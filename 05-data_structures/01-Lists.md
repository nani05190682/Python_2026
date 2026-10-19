# Lists in Python
## Work with Ordered Collections

### 1. What Are Lists?

A **list** is a built-in Python data structure that stores multiple items in a specific order.

Think of a list as a container that holds related information.

Real-world examples include:
- **Shopping list:** Milk, eggs, bread.
- **To-do list:** Tasks arranged in order.
- **Playlist:** Songs in sequence.
- **Server inventory:** Names of servers in an environment.
- **Student records:** A collection of student names.

Lists are one of the most commonly used data structures in Python because they are flexible and easy to work with.

### 2. Creating Lists

Python uses square brackets (`[]`) to create lists. Items are separated by commas.

#### A. Creating an empty list

```python
my_list = []

print(my_list)
```

Output:

```text
[]
```

An empty list is useful when you plan to add items later.

#### B. Creating a list with items

```python
fruits = ["apple", "banana", "orange"]
numbers = [1, 2, 3, 4, 5]

print(fruits)
print(numbers)
```

Output:

```text
['apple', 'banana', 'orange']
[1, 2, 3, 4, 5]
```

#### C. Storing different data types

A list can contain values of different data types.

```python
mixed = ["hello", 42, True, 3.14]

print(mixed)
```

Output:

```text
['hello', 42, True, 3.14]
```

Although Python allows mixed data types, lists are often easier to manage when their items serve a similar purpose.

#### D. Creating a list using `list()`

Python provides the `list()` constructor to create a list from an iterable.

```python
letters = list("Python")

print(letters)
```

Output:

```text
['P', 'y', 't', 'h', 'o', 'n']
```

This converts the string into a list containing individual characters.

### 3. Accessing List Items

Each item in a list has an index. Python uses zero-based indexing, which means the first item has index `0`.

```python
fruits = ["apple", "banana", "orange"]

print(fruits[0])
print(fruits[1])
print(fruits[2])
```

Output:

```text
apple
banana
orange
```

You can also access items from the end using negative indexes.

```python
fruits = ["apple", "banana", "orange"]

print(fruits[-1])
print(fruits[-2])
```

Output:

```text
orange
banana
```

| Index | Value |
|---:|---|
| `0` | `"apple"` |
| `1` | `"banana"` |
| `2` or `-1` | `"orange"` |
| `-2` | `"banana"` |

**Important:** Accessing an index that does not exist raises an `IndexError`.

### 4. Slicing Lists

Slicing allows you to extract a portion of a list.

The syntax is:

```python
list_name[start:stop:step]
```

- `start` is the index where slicing begins.
- `stop` is the index where slicing ends, but it is excluded.
- `step` determines how many positions to move between items.

#### A. Selecting a range of items

```python
fruits = ["apple", "banana", "orange", "mango"]

print(fruits[0:2])
print(fruits[1:3])
```

Output:

```text
['apple', 'banana']
['banana', 'orange']
```

#### B. Selecting items from a starting position

```python
fruits = ["apple", "banana", "orange", "mango"]

print(fruits[1:])
```

Output:

```text
['banana', 'orange', 'mango']
```

#### C. Selecting items up to a position

```python
fruits = ["apple", "banana", "orange", "mango"]

print(fruits[:2])
```

Output:

```text
['apple', 'banana']
```

#### D. Selecting every second item

```python
numbers = [0, 1, 2, 3, 4, 5, 6]

print(numbers[::2])
```

Output:

```text
[0, 2, 4, 6]
```

Slicing is useful when you need to process only part of a collection.

### 5. Modifying Lists

Lists are **mutable**, which means you can change their contents after creation.

#### A. Changing an item

```python
fruits = ["apple", "banana", "orange"]

fruits[0] = "mango"

print(fruits)
```

Output:

```text
['mango', 'banana', 'orange']
```

The first item has been replaced with `"mango"`.

#### B. Adding an item using `append()`

The `append()` method adds an item to the end of a list.

```python
fruits = ["apple", "banana"]

fruits.append("orange")

print(fruits)
```

Output:

```text
['apple', 'banana', 'orange']
```

#### C. Inserting an item using `insert()`

The `insert()` method adds an item at a specified index.

```python
fruits = ["apple", "orange"]

fruits.insert(1, "banana")

print(fruits)
```

Output:

```text
['apple', 'banana', 'orange']
```

The existing items move to make room for the new item.

#### D. Adding multiple items using `extend()`

The `extend()` method adds all items from another iterable to the end of the list.

```python
fruits = ["apple", "banana"]

fruits.extend(["orange", "mango"])

print(fruits)
```

Output:

```text
['apple', 'banana', 'orange', 'mango']
```

Unlike `append()`, which adds its argument as one item, `extend()` adds each item from the iterable.

```python
numbers = [1, 2]

numbers.append([3, 4])
print(numbers)
```

Output:

```text
[1, 2, [3, 4]]
```

Here, `[3, 4]` becomes a single nested list item.

### 6. Removing Items from Lists

Python provides several ways to remove list items.

#### A. Using `remove()`

The `remove()` method removes the first occurrence of a specified value.

```python
fruits = ["apple", "banana", "orange"]

fruits.remove("banana")

print(fruits)
```

Output:

```text
['apple', 'orange']
```

If the value does not exist, `remove()` raises a `ValueError`.

#### B. Using `pop()`

The `pop()` method removes and returns an item. By default, it removes the last item.

```python
fruits = ["apple", "banana", "orange"]

last_fruit = fruits.pop()

print(last_fruit)
print(fruits)
```

Output:

```text
orange
['apple', 'banana']
```

You can also provide an index.

```python
fruits = ["apple", "banana", "orange"]

removed_fruit = fruits.pop(1)

print(removed_fruit)
print(fruits)
```

Output:

```text
banana
['apple', 'orange']
```

#### C. Using `del`

The `del` statement removes an item by index.

```python
fruits = ["apple", "banana", "orange"]

del fruits[0]

print(fruits)
```

Output:

```text
['banana', 'orange']
```

You can also delete a slice or the entire list variable.

#### D. Using `clear()`

The `clear()` method removes all items but keeps the list itself.

```python
fruits = ["apple", "banana", "orange"]

fruits.clear()

print(fruits)
```

Output:

```text
[]
```

### 7. Useful List Functions and Methods

Python provides built-in functions and list methods to help you inspect and manipulate collections.

```python
numbers = [3, 1, 4, 1, 5, 9]

print(len(numbers))
print(numbers.count(1))
print(numbers.index(4))
print(min(numbers))
print(max(numbers))
print(sum(numbers))
```

Output:

```text
6
2
2
1
9
23
```

| Function or method | Purpose |
|---|---|
| `len(numbers)` | Returns the number of items |
| `numbers.count(1)` | Counts occurrences of a value |
| `numbers.index(4)` | Finds the index of the first matching value |
| `min(numbers)` | Returns the smallest item |
| `max(numbers)` | Returns the largest item |
| `sum(numbers)` | Adds numeric items together |

Remember that `index()` raises a `ValueError` if the specified value is not found.

### 8. Sorting and Reversing Lists

#### A. Sorting in ascending order

The `sort()` method sorts a list in place, modifying the original list.

```python
numbers = [3, 1, 4, 1, 5, 9]

numbers.sort()

print(numbers)
```

Output:

```text
[1, 1, 3, 4, 5, 9]
```

#### B. Sorting in descending order

```python
numbers = [3, 1, 4, 1, 5, 9]

numbers.sort(reverse=True)

print(numbers)
```

Output:

```text
[9, 5, 4, 3, 1, 1]
```

#### C. Reversing a list

The `reverse()` method reverses the current order of items. It does not sort them.

```python
numbers = [3, 1, 4, 1, 5, 9]

numbers.reverse()

print(numbers)
```

Output:

```text
[9, 5, 1, 4, 1, 3]
```

#### D. Creating a sorted copy

If you want to keep the original list unchanged, use the built-in `sorted()` function.

```python
numbers = [3, 1, 4, 1, 5, 9]

sorted_numbers = sorted(numbers)

print("Original:", numbers)
print("Sorted:", sorted_numbers)
```

Output:

```text
Original: [3, 1, 4, 1, 5, 9]
Sorted: [1, 1, 3, 4, 5, 9]
```

**Important:** Methods such as `sort()`, `reverse()`, `append()`, and `clear()` modify the list and return `None`. Do not assign their return values back to the list.

### 9. Copying Lists

You can copy a list using the `copy()` method or slicing.

```python
original = ["Python", "Linux", "Docker"]

copied = original.copy()

copied.append("Kubernetes")

print("Original:", original)
print("Copied:", copied)
```

Output:

```text
Original: ['Python', 'Linux', 'Docker']
Copied: ['Python', 'Linux', 'Docker', 'Kubernetes']
```

The original list remains unchanged when you add an item to this copied list.

However, `copy()` creates a **shallow copy**. If the list contains other mutable objects, such as nested lists, those inner objects are still shared.

Example:

```python
original = [[1, 2], [3, 4]]
copied = original.copy()

copied[0].append(99)

print(original)
print(copied)
```

Output:

```text
[[1, 2, 99], [3, 4]]
[[1, 2, 99], [3, 4]]
```

Both lists reflect the change because their first elements refer to the same inner list. You will learn more about shallow and deep copying as you advance in Python.

### 10. Checking Whether an Item Exists

Use the `in` operator to check whether a list contains a value.

```python
fruits = ["apple", "banana", "orange"]

if "apple" in fruits:
    print("Found apple!")
else:
    print("Apple not found.")
```

Output:

```text
Found apple!
```

You can also use `not in`.

```python
fruits = ["apple", "banana", "orange"]

if "mango" not in fruits:
    print("Mango is not in the list.")
```

Output:

```text
Mango is not in the list.
```

#### Checking whether a list is empty

An empty list evaluates to `False` in a Boolean context. A non-empty list evaluates to `True`.

```python
tasks = []

if tasks:
    print("The list contains tasks.")
else:
    print("The list is empty.")
```

Output:

```text
The list is empty.
```

This is a common Python pattern for checking whether a collection has items.

### 11. Looping Through Lists

Lists work naturally with `for` loops.

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

You can also access each item's index using `enumerate()`.

```python
servers = ["web-01", "web-02", "db-01"]

for index, server in enumerate(servers):
    print(index, server)
```

Output:

```text
0 web-01
1 web-02
2 db-01
```

To start counting from `1`, provide the `start` argument:

```python
for index, server in enumerate(servers, start=1):
    print(index, server)
```

Output:

```text
1 web-01
2 web-02
3 db-01
```

### 12. Common Mistakes to Avoid

**Mistake 1: Accessing an index that does not exist**

```python
fruits = ["apple", "banana"]

# print(fruits[2])  # Raises IndexError
```

The valid indexes are `0` and `1`.

**Mistake 2: Confusing `append()` and `extend()`**

```python
numbers = [1, 2]

numbers.append([3, 4])

print(numbers)
```

Output:

```text
[1, 2, [3, 4]]
```

Use `extend()` if you want to add the individual items:

```python
numbers = [1, 2]

numbers.extend([3, 4])

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

**Mistake 3: Modifying a list while iterating over it**

Removing items from a list while iterating over that same list can cause items to be skipped.

A safer approach is to build a new list:

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [
    number for number in numbers
    if number % 2 == 0
]

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

This technique is called a list comprehension. You will explore it in a later lesson.

### 13. Practice Exercises

Create a Python file named `lists_practice.py` and complete these tasks.

**Task 1: Create a list**

Create a list of five programming languages and print the list.

**Task 2: Access elements**

Print the first, third, and last items from your list.

**Task 3: Modify a list**

Replace the second language with `"Python"`. Add `"Go"` to the end and insert `"Java"` at index `1`.

**Task 4: Remove items**

Remove one item by value and another by index.

**Task 5: Perform calculations**

Given the list below, calculate its length, sum, minimum, and maximum.

```python
numbers = [10, 20, 30, 40, 50]
```

**Task 6: Sort values**

Sort the following list in ascending order and then in descending order.

```python
scores = [75, 90, 65, 85, 70]
```

**Task 7: Filter values**

Create a new list containing only the even numbers from this list.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**Task 8: Manage a server inventory**

Create a list of server names. Add a new server, remove a decommissioned server, and print all remaining servers using a loop.

### 14. Sample Solution

```python
# Task 1: Create a list
languages = ["Python", "Java", "C++", "JavaScript", "Go"]
print(languages)

# Task 2: Access elements
print(languages[0])
print(languages[2])
print(languages[-1])

# Task 3: Modify a list
languages[1] = "Python"
languages.append("Rust")
languages.insert(1, "Java")

print(languages)

# Task 4: Remove items
languages.remove("C++")
removed_language = languages.pop(0)

print("Removed:", removed_language)
print("Remaining:", languages)

# Task 5: Perform calculations
numbers = [10, 20, 30, 40, 50]

print("Length:", len(numbers))
print("Sum:", sum(numbers))
print("Minimum:", min(numbers))
print("Maximum:", max(numbers))

# Task 6: Sort values
scores = [75, 90, 65, 85, 70]

scores.sort()
print("Ascending:", scores)

scores.sort(reverse=True)
print("Descending:", scores)

# Task 7: Filter even numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

even_numbers = [
    number for number in numbers
    if number % 2 == 0
]

print("Even numbers:", even_numbers)

# Task 8: Manage a server inventory
servers = ["web-01", "web-02", "db-01"]

servers.append("app-01")
servers.remove("web-02")

for server in servers:
    print(f"Active inventory item: {server}")
```

### 15. Summary

In this lesson, you learned:

- Lists store ordered collections of items.
- Lists can contain duplicate values and different data types.
- Indexing and slicing help you access specific items.
- Lists are mutable, so you can modify them after creation.
- `append()`, `insert()`, and `extend()` add items.
- `remove()`, `pop()`, `del`, and `clear()` remove items.
- `sort()` and `reverse()` modify the list's order.
- `copy()` creates a shallow copy.
- `in` and `not in` check membership.
- Loops let you process each item in a list.

### What's Next?

**Dictionaries in Python — Store Information Using Key-Value Pairs**

Learn how to organize related information, access values by key, add and update entries, and use dictionaries to represent structured data such as server configurations and student records.
