# Data Structures in Python
## Store Multiple Values Together

### 1. Introduction to Data Structures

So far, you have learned how to store individual values in variables.

For example:

```python
name = "Alice"
age = 25
city = "Bengaluru"
```

This works well when you have only a few values. But what if you need to store information about 100 students, manage thousands of server names, or process a collection of log entries?

Creating a separate variable for every value would become difficult to manage.

Python provides **data structures** that allow you to organize and work with multiple values efficiently.

Example:

```python
students = ["Alice", "Bob", "Charlie", "David"]

print(students)
```

Output:

```text
['Alice', 'Bob', 'Charlie', 'David']
```

Instead of creating four separate variables, we store all four names in one list.

### 2. The Four Main Python Data Structures

Python provides four commonly used built-in collection types:

<box gap={3}>
  <row align=start gap={3}>
    <box size="76px" radius="lg" background="surface-secondary" align=center justify=center>
      <icon name="list" size="2xl"/>
    </box>
    <box flex="1" gap={1}>
      **1. Lists (`list`)**

      Lists store ordered collections of items. You can add, remove, and modify elements.

      Example: A list of students, server names, or course topics.

      ```python
      courses = ["Python", "Linux", "Docker"]
      ```
    </box>
  </row>
  <divider color="subtle"/>
  <row align=start gap={3}>
    <box size="76px" radius="lg" background="surface-secondary" align=center justify=center>
      <icon name="book-open" size="2xl"/>
    </box>
    <box flex="1" gap={1}>
      **2. Dictionaries (`dict`)**

      Dictionaries store key-value pairs. You use a key to look up its associated value.

      Example: Storing a student's name and age, or a server's name and IP address.

      ```python
      student = {"name": "Alice", "age": 25}
      ```
    </box>
  </row>
  <divider color="subtle"/>
  <row align=start gap={3}>
    <box size="76px" radius="lg" background="surface-secondary" align=center justify=center>
      <icon name="map-pin" size="2xl"/>
    </box>
    <box flex="1" gap={1}>
      **3. Tuples (`tuple`)**

      Tuples store ordered collections of items. They cannot be modified after creation.

      Example: Representing coordinates or a fixed configuration.

      ```python
      coordinates = (12.97, 77.59)
      ```
    </box>
  </row>
  <divider color="subtle"/>
  <row align=start gap={3}>
    <box size="76px" radius="lg" background="surface-secondary" align=center justify=center>
      <icon name="layers" size="2xl"/>
    </box>
    <box flex="1" gap={1}>
      **4. Sets (`set`)**

      Sets store unique elements. They are useful for removing duplicates and checking membership.

      Example: Maintaining a collection of unique usernames or IP addresses.

      ```python
      unique_tools = {"Linux", "Docker", "Python"}
      ```
    </box>
  </row>
</box>

### 3. Comparing the Four Data Structures

| Feature | List | Dictionary | Tuple | Set |
|---|---|---|---|---|
| Stores multiple values | Yes | Yes, as key-value pairs | Yes | Yes |
| Maintains order | Yes | Yes, insertion order | Yes | No guaranteed order |
| Allows duplicate values | Yes | Keys must be unique; values may repeat | Yes | No duplicate elements |
| Can be modified | Yes | Yes | No | Yes |
| Access method | Index | Key | Index | Membership or iteration |
| Syntax | `[]` | `{key: value}` | `()` | `{}` |

**Important:** An empty dictionary is written as `{}`, while an empty set is written as `set()`.

### 4. Which Data Structure Should You Use?

Choose a data structure based on what you need to do with your data.

- **Use a list** when you need an ordered collection that can change.
- **Use a dictionary** when you need to look up values using meaningful keys.
- **Use a tuple** when you need an ordered collection that should remain unchanged.
- **Use a set** when you need unique elements and set operations.

For example, in a DevOps automation project:

```python
# A collection of servers
servers = ["web-01", "web-02", "db-01"]

# Information about one server
server = {
    "name": "web-01",
    "ip": "192.168.1.10",
    "status": "running"
}

# Fixed coordinates
location = (12.97, 77.59)

# Unique tools
tools = {"Linux", "Docker", "Python"}
```

Each structure serves a different purpose.

### 5. Understanding Indexing

Python uses **zero-based indexing** for ordered sequences such as lists and tuples. This means the first element has index `0`, the second has index `1`, and so on.

Example:

```python
languages = ["Python", "Java", "Go", "Rust"]

print(languages[0])
print(languages[1])
print(languages[2])
print(languages[3])
```

Output:

```text
Python
Java
Go
Rust
```

You can also access elements from the end using negative indexes.

```python
languages = ["Python", "Java", "Go", "Rust"]

print(languages[-1])
print(languages[-2])
```

Output:

```text
Rust
Go
```

Remember that using an index outside the valid range of a list or tuple raises an `IndexError`.

### 6. Learning Path

You will learn these structures one at a time, starting with lists.

<box border radius="lg" padding={3} gap={3}>
  <row align=center gap={3}>
    <box background="surface-secondary" radius="md" size="40px" align=center justify=center>
      <icon name="list" size="lg"/>
    </box>
    <box flex="1" gap={1}>
      **Lesson 1: Lists**
      <text color="secondary" size="sm">Create lists, access elements, add and remove items, and loop through collections.</text>
    </box>
    <badge color="success">Start here</badge>
  </row>
  <divider color="subtle"/>
  <row align=center gap={3}>
    <box background="surface-secondary" radius="md" size="40px" align=center justify=center>
      <icon name="book-open" size="lg"/>
    </box>
    <box flex="1" gap={1}>
      **Lesson 2: Dictionaries**
      <text color="secondary" size="sm">Store structured information using key-value pairs.</text>
    </box>
  </row>
  <divider color="subtle"/>
  <row align=center gap={3}>
    <box background="surface-secondary" radius="md" size="40px" align=center justify=center>
      <icon name="map-pin" size="lg"/>
    </box>
    <box flex="1" gap={1}>
      **Lesson 3: Tuples**
      <text color="secondary" size="sm">Work with ordered collections that cannot be modified.</text>
    </box>
  </row>
  <divider color="subtle"/>
  <row align=center gap={3}>
    <box background="surface-secondary" radius="md" size="40px" align=center justify=center>
      <icon name="layers" size="lg"/>
    </box>
    <box flex="1" gap={1}>
      **Lesson 4: Sets**
      <text color="secondary" size="sm">Remove duplicates and perform union, intersection, and difference operations.</text>
    </box>
  </row>
</box>

### Summary

In this introduction, you learned:

- Why data structures are useful for organizing multiple values.
- The four main collection types: lists, dictionaries, tuples, and sets.
- How their ordering, mutability, and duplicate-handling behavior differs.
- How zero-based indexing works for lists and tuples.
- How to select a data structure based on your requirements.

### What's Next?

**Lesson 1: Lists in Python — Store and Manage Collections of Data**

Let's learn how to create lists, access individual elements, modify values, add and remove items, and process collections using loops.
