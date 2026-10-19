# Python Dictionaries
## Store Data Using Key-Value Pairs

### 1. What Are Dictionaries?

A **dictionary** is a Python data structure that stores information as **key-value pairs**. It allows you to retrieve information using a key instead of remembering its position.

Think of a real-world dictionary: you look up a word to find its meaning. Similarly, in Python, you use a key to retrieve its corresponding value.

**Real-world examples:**

- Phone book: name → phone number
- Restaurant menu: dish → price
- User profile: username → user information
- Server configuration: setting → configured value

For example, a server configuration might look like this:

```python
server = {
    "hostname": "web-server-01",
    "ip_address": "192.168.1.10",
    "port": 8080,
    "status": "running"
}

print(server["hostname"])
print(server["status"])
```

**Output:**
```text
web-server-01
running
```

Here, `"hostname"` and `"status"` are keys, while `"web-server-01"` and `"running"` are their corresponding values.

### 2. Creating Dictionaries

Dictionaries use curly braces `{}` and separate each key from its value using a colon (`:`).

#### Creating an empty dictionary

```python
my_dict = {}

print(my_dict)
print(type(my_dict))
```

**Output:**
```text
{}
<class 'dict'>
```

#### Creating a dictionary with data

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

print(person)
```

**Output:**
```text
{'name': 'Alice', 'age': 30, 'city': 'New York'}
```

#### Creating a dictionary using `dict()`

```python
scores = dict(math=95, english=87, science=92)

print(scores)
```

**Output:**
```text
{'math': 95, 'english': 87, 'science': 92}
```

When using this form, the keys are written as keyword arguments, so they must be valid Python identifiers.

#### Important dictionary rules

1. Keys must be unique.
2. Values can be duplicated.
3. Keys must be hashable, such as strings, integers, or tuples containing only hashable values.
4. Values can be of different data types.
5. Dictionaries are mutable, meaning you can add, update, and remove items.
6. In modern Python, dictionaries preserve insertion order.

Example:

```python
data = {
    "name": "Alice",
    "age": 30,
    "name": "Bob"
}

print(data)
```

**Output:**
```text
{'name': 'Bob', 'age': 30}
```

The second `"name"` entry replaces the first because dictionary keys must be unique.

### 3. Accessing Dictionary Values

You can retrieve a value by specifying its key inside square brackets `[]`.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

print(person["name"])
print(person["age"])
print(person["city"])
```

**Output:**
```text
Alice
30
New York
```

#### What happens if a key doesn't exist?

Accessing a missing key with square brackets raises a `KeyError`.

```python
person = {"name": "Alice"}

print(person["job"])
```

**Output:**
```text
KeyError: 'job'
```

To avoid this error when a key might be missing, use the `get()` method.

#### Using `get()`

```python
person = {"name": "Alice", "age": 30}

print(person.get("name"))
print(person.get("job"))
print(person.get("job", "Unknown"))
```

**Output:**
```text
Alice
None
Unknown
```

The `get()` method returns `None` when the key is missing, unless you provide a default value.

**Remember:**
- `person["job"]` → raises `KeyError` if `"job"` doesn't exist.
- `person.get("job")` → returns `None` if `"job"` doesn't exist.
- `person.get("job", "Unknown")` → returns `"Unknown"` if `"job"` doesn't exist.

### 4. Adding and Updating Dictionary Items

Dictionaries allow you to add new key-value pairs or update existing values.

#### Adding a new item

```python
person = {
    "name": "Alice",
    "age": 30
}

person["email"] = "alice@example.com"

print(person)
```

**Output:**
```text
{'name': 'Alice', 'age': 30, 'email': 'alice@example.com'}
```

Because `"email"` did not exist, Python added a new item.

#### Updating an existing item

```python
person = {
    "name": "Alice",
    "age": 30
}

person["age"] = 31

print(person)
```

**Output:**
```text
{'name': 'Alice', 'age': 31}
```

Because `"age"` already existed, Python updated its value.

#### Updating multiple items

Use `update()` to add or modify several items at once.

```python
person = {
    "name": "Alice",
    "age": 30
}

person.update({
    "age": 31,
    "job": "Engineer",
    "city": "Bengaluru"
})

print(person)
```

**Output:**
```text
{'name': 'Alice', 'age': 31, 'job': 'Engineer', 'city': 'Bengaluru'}
```

The existing `"age"` value was updated, while `"job"` and `"city"` were added.

### 5. Removing Dictionary Items

Python provides several ways to remove items from a dictionary.

#### Using `del`

Removes an item using its key.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

del person["city"]

print(person)
```

**Output:**
```text
{'name': 'Alice', 'age': 30}
```

If the key does not exist, `del` raises a `KeyError`.

#### Using `pop()`

Removes an item and returns its value.

```python
person = {
    "name": "Alice",
    "age": 30
}

removed_age = person.pop("age")

print(removed_age)
print(person)
```

**Output:**
```text
30
{'name': 'Alice'}
```

You can also supply a default value to avoid an error when the key is missing.

```python
person = {"name": "Alice"}

job = person.pop("job", "Not specified")

print(job)
```

**Output:**
```text
Not specified
```

#### Using `clear()`

Removes all items but keeps the dictionary itself.

```python
person = {
    "name": "Alice",
    "age": 30
}

person.clear()

print(person)
```

**Output:**
```text
{}
```

### 6. Useful Dictionary Methods

Let's explore some commonly used dictionary methods.

#### `keys()` — Get all keys

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "Bengaluru"
}

print(person.keys())
```

**Output:**
```text
dict_keys(['name', 'age', 'city'])
```

#### `values()` — Get all values

```python
print(person.values())
```

**Output:**
```text
dict_values(['Alice', 30, 'Bengaluru'])
```

#### `items()` — Get key-value pairs

```python
print(person.items())
```

**Output:**
```text
dict_items([('name', 'Alice'), ('age', 30), ('city', 'Bengaluru')])
```

These methods return dictionary views, not ordinary lists. You can convert them to lists when needed:

```python
print(list(person.keys()))
print(list(person.values()))
print(list(person.items()))
```

#### Checking whether a key exists

Use the `in` operator to check whether a key is present.

```python
person = {
    "name": "Alice",
    "age": 30
}

if "name" in person:
    print("Name found!")

if "job" not in person:
    print("Job information is missing.")
```

**Output:**
```text
Name found!
Job information is missing.
```

By default, `in` checks dictionary keys, not values.

#### Getting the number of items

Use `len()` to count the number of key-value pairs.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "Bengaluru"
}

print(len(person))
```

**Output:**
```text
3
```

### 7. Looping Through Dictionaries

Loops let you process dictionary data one item at a time.

#### Loop through keys

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "Bengaluru"
}

for key in person:
    print(key)
```

**Output:**
```text
name
age
city
```

#### Loop through values

```python
for value in person.values():
    print(value)
```

**Output:**
```text
Alice
30
Bengaluru
```

#### Loop through keys and values

Use `items()` when you need both the key and its value.

```python
for key, value in person.items():
    print(f"{key}: {value}")
```

**Output:**
```text
name: Alice
age: 30
city: Bengaluru
```

This technique is especially useful when processing configuration files, user profiles, application settings, and monitoring data.

### 8. Nested Dictionaries

A nested dictionary is a dictionary stored inside another dictionary. It is useful for representing structured information.

For example, let's store information about multiple students.

```python
students = {
    "alice": {
        "age": 20,
        "grade": "A"
    },
    "bob": {
        "age": 21,
        "grade": "B"
    },
    "charlie": {
        "age": 19,
        "grade": "A"
    }
}

print(students["alice"]["grade"])
print(students["bob"]["age"])
```

**Output:**
```text
A
21
```

The first expression works in two steps:

1. `students["alice"]` retrieves Alice's dictionary.
2. `["grade"]` retrieves the grade from that dictionary.

#### Practical example: Server inventory

```python
servers = {
    "web01": {
        "ip": "192.168.1.10",
        "status": "running",
        "cpu": 45
    },
    "db01": {
        "ip": "192.168.1.20",
        "status": "stopped",
        "cpu": 0
    }
}

print(servers["web01"]["ip"])
print(servers["db01"]["status"])
```

**Output:**
```text
192.168.1.10
stopped
```

This structure can help an SRE or DevOps engineer organize server inventory, service status, resource utilization, or environment configuration.

### 9. Common Mistakes

**Mistake 1: Accessing a key that doesn't exist**

Incorrect:

```python
person = {"name": "Alice"}
print(person["age"])
```

This raises `KeyError`.

Better:

```python
print(person.get("age", "Age not available"))
```

**Mistake 2: Using a mutable object as a key**

Incorrect:

```python
data = {
    ["name", "age"]: "person"
}
```

Lists cannot be dictionary keys because they are mutable and unhashable.

Correct:

```python
data = {
    ("name", "age"): "person"
}

print(data[("name", "age")])
```

**Output:**
```text
person
```

Tuples can be keys if all their elements are hashable.

**Mistake 3: Assuming `in` checks values**

```python
person = {"name": "Alice"}

print("Alice" in person)
```

**Output:**
```text
False
```

The `in` operator checks keys by default.

To check values:

```python
print("Alice" in person.values())
```

**Output:**
```text
True
```

**Mistake 4: Confusing a key with a variable**

```python
name = "Alice"

person = {
    "name": name
}

print(person["name"])
```

**Output:**
```text
Alice
```

Here, `"name"` is the dictionary key, while `name` is a Python variable whose value is `"Alice"`.

### 10. Practice Exercises

Try these exercises before looking at the solutions.

**Exercise 1: Create a dictionary**

Create a dictionary called `employee` with these details:

- Name: Ravi
- Age: 35
- Department: DevOps
- Salary: 120000

Print the employee's name and department.

**Exercise 2: Add and update**

Starting with:

```python
employee = {
    "name": "Ravi",
    "age": 35
}
```

Add an `"email"` key and update the age to `36`. Print the dictionary.

**Exercise 3: Check whether a key exists**

Write a program that checks whether `"email"` exists in the following dictionary:

```python
employee = {
    "name": "Ravi",
    "age": 35
}
```

Print `"Email found"` if it exists; otherwise, print `"Email not found"`.

**Exercise 4: Loop through a dictionary**

Given:

```python
services = {
    "nginx": "running",
    "mysql": "stopped",
    "redis": "running"
}
```

Print each service name and its status using a loop.

**Exercise 5: Nested dictionaries**

Create a dictionary containing two servers, `web01` and `db01`. Store each server's IP address and status. Print the IP address of `web01` and the status of `db01`.

### 11. Sample Solutions

**Solution 1**

```python
employee = {
    "name": "Ravi",
    "age": 35,
    "department": "DevOps",
    "salary": 120000
}

print(employee["name"])
print(employee["department"])
```

**Solution 2**

```python
employee = {
    "name": "Ravi",
    "age": 35
}

employee["email"] = "ravi@example.com"
employee["age"] = 36

print(employee)
```

**Solution 3**

```python
employee = {
    "name": "Ravi",
    "age": 35
}

if "email" in employee:
    print("Email found")
else:
    print("Email not found")
```

**Solution 4**

```python
services = {
    "nginx": "running",
    "mysql": "stopped",
    "redis": "running"
}

for service, status in services.items():
    print(f"{service}: {status}")
```

**Solution 5**

```python
servers = {
    "web01": {
        "ip": "192.168.1.10",
        "status": "running"
    },
    "db01": {
        "ip": "192.168.1.20",
        "status": "stopped"
    }
}

print(servers["web01"]["ip"])
print(servers["db01"]["status"])
```

### 12. Quick Summary

| Concept | Purpose |
|---|---|
| `{}` | Create an empty dictionary |
| `person["name"]` | Access a value by key |
| `person.get("name")` | Safely retrieve a value |
| `person["email"] = value` | Add or update an item |
| `del person["name"]` | Remove an item |
| `person.pop("age")` | Remove an item and return its value |
| `person.keys()` | Get the keys |
| `person.values()` | Get the values |
| `person.items()` | Get key-value pairs |
| `"name" in person` | Check whether a key exists |
| `person.update({...})` | Add or update multiple items |
| `len(person)` | Count the items |

**Key takeaway:** Use dictionaries when you want to organize data by meaningful labels rather than numerical positions. They are especially useful for configuration, API responses, user profiles, JSON data, and automation scripts.

### What's Next?

**Tuples in Python — Store Ordered Data That Cannot Be Changed**

You'll learn how tuples differ from lists, how to create them, access their elements, and use them when data should remain unchanged.
