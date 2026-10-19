# Your First Python Class — Create a Simple Class

## 1. Introduction

In the previous lesson, you learned that a **class is a blueprint for creating objects**.

Now, let's build your first class step by step.

By the end of this lesson, you will know how to:

- Define a class using the `class` keyword.
- Initialize objects using `__init__()`.
- Understand the purpose of `self`.
- Create multiple objects from one class.
- Access and modify object attributes.
- Avoid common mistakes when creating classes.

## 2. How Classes Work

Working with classes follows four basic steps:

1. **Define the class:** Create a blueprint using the `class` keyword.
2. **Initialize the object:** Set up its initial data using `__init__()`.
3. **Create instances:** Create objects from the class.
4. **Access the data:** Read or modify the attributes of each object.

Let's explore each step.

## 3. Define Your First Class

Every Python class starts with the `class` keyword.

```python
class Dog:
    pass
```

### Understanding the code

- `class` tells Python that you are defining a class.
- `Dog` is the name of the class.
- `pass` is a placeholder that allows the class body to remain empty.

Python conventionally uses **PascalCase** for class names. Each word begins with a capital letter, as in `Dog`, `StudentRecord`, and `APIConfig`.

### Create an object

```python
class Dog:
    pass


dog1 = Dog()

print(type(dog1))
```

Output:

```text
<class '__main__.Dog'>
```

The variable `dog1` refers to an object created from the `Dog` class.

You can create multiple objects from the same class:

```python
dog1 = Dog()
dog2 = Dog()

print(type(dog1))
print(type(dog2))
```

Both objects belong to the same class, but they are separate instances.

## 4. Add an Initializer Using `__init__()`

An empty class is not very useful when you want to store information about an object.

For example, every dog has a name and a breed.

We can use the `__init__()` method to initialize these attributes.

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed
```

Now create some dog objects:

```python
dog1 = Dog("Buddy", "Golden Retriever")
dog2 = Dog("Max", "Beagle")
dog3 = Dog(name="Charlie", breed="Poodle")

print(dog1.name)
print(dog2.breed)
print(dog3.name)
```

Output:

```text
Buddy
Beagle
Charlie
```

### Understanding `__init__()`

The `__init__()` method initializes an object when it is created.

Consider this line:

```python
dog1 = Dog("Buddy", "Golden Retriever")
```

Python creates a new `Dog` object and calls its initializer with that object, `"Buddy"`, and `"Golden Retriever"`.

Inside the initializer:

```python
self.name = name
self.breed = breed
```

- `name` receives the value `"Buddy"`.
- `breed` receives the value `"Golden Retriever"`.
- `self.name` stores the name on the particular dog object.
- `self.breed` stores the breed on that object.

**What does `__init__` mean?**

The name `__init__` has two underscores at the beginning and two at the end. Methods with this naming pattern are often called *dunder methods*, short for *double underscore methods*.

Although it is commonly described as the constructor in beginner tutorials, technically `__init__()` initializes an object that Python has already created.

You must spell `__init__` exactly as shown.

## 5. Understanding `self`

`self` refers to the current instance of a class.

It allows an object to access and store its own attributes.

Consider this example:

```python
class Dog:
    def __init__(self, name):
        self.name = name


dog1 = Dog("Buddy")
dog2 = Dog("Max")

print(dog1.name)
print(dog2.name)
```

Output:

```text
Buddy
Max
```

Each object stores its own name.

### How `self` works

When Python executes:

```python
dog1 = Dog("Buddy")
```

The initializer stores `"Buddy"` in the `name` attribute of the new object.

When Python executes:

```python
dog2 = Dog("Max")
```

It stores `"Max"` in the second object's `name` attribute.

Therefore:

- `dog1.name` is `"Buddy"`.
- `dog2.name` is `"Max"`.

### Do you pass `self` when creating an object?

No. Python passes the instance automatically when calling an ordinary instance method through an object.

For example:

```python
class Dog:
    def __init__(self, name):
        self.name = name


dog1 = Dog("Buddy")
```

You provide `"Buddy"`, not `self`.

**Important:** `self` is a convention rather than a reserved Python keyword. Nevertheless, always use `self` as the first parameter of ordinary instance methods to follow standard Python practices.

## 6. Positional and Keyword Arguments

When creating an object, you can pass arguments positionally or by name.

### Positional arguments

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed


dog1 = Dog("Buddy", "Golden Retriever")
```

Python matches the first argument to `name` and the second to `breed`.

### Keyword arguments

```python
dog2 = Dog(name="Max", breed="Beagle")
```

Keyword arguments explicitly identify which parameter receives each value.

You can also mix positional and keyword arguments, provided positional arguments come first:

```python
dog3 = Dog("Charlie", breed="Poodle")
```

Keyword arguments are often easier to read when a class has several parameters.

## 7. Real-World Example — API Configuration

Classes are useful for grouping related configuration data in AI engineering, cloud automation, and API development.

Let's create a class that stores API configuration.

```python
class APIConfig:
    def __init__(
        self,
        api_key,
        model="example-model",
        max_tokens=100
    ):
        self.api_key = api_key
        self.model = model
        self.max_tokens = max_tokens
        self.base_url = "https://api.openai.com/v1"


dev_config = APIConfig(
    api_key="development-placeholder",
    max_tokens=50
)

prod_config = APIConfig(
    api_key="production-placeholder",
    model="production-model",
    max_tokens=1000
)

print(dev_config.model)
print(prod_config.model)
print(prod_config.max_tokens)
```

Output:

```text
example-model
production-model
1000
```

The model names here are illustrative configuration values; they are not claims about currently available models.

### Understanding default parameters

Notice this definition:

```python
def __init__(
    self,
    api_key,
    model="example-model",
    max_tokens=100
):
```

Here:

- `api_key` is required.
- `model` has a default value.
- `max_tokens` has a default value.

When you create `dev_config`, you do not supply `model` or `max_tokens`, so Python uses their default values unless overridden.

For `prod_config`, you provide both optional values explicitly.

### Security note

The example uses placeholder strings instead of real API keys.

In production applications, load credentials from environment variables or a suitable secrets manager. Avoid committing real API keys to source control.

## 8. Class Versus Instance

Understanding the difference between a class and an instance is essential.

| Concept | Example | Meaning |
|---|---|---|
| Class | `APIConfig` | The blueprint |
| Instance | `config1` | An object created from the blueprint |
| Instance attribute | `config1.max_tokens` | Data stored on that particular object |
| Initializer | `__init__()` | Sets up initial object data |

### Example: Multiple instances

```python
class APIConfig:
    def __init__(self, api_key, max_tokens=100):
        self.api_key = api_key
        self.max_tokens = max_tokens


config1 = APIConfig("key-placeholder-1", max_tokens=50)
config2 = APIConfig("key-placeholder-2", max_tokens=200)

print(config1.max_tokens)
print(config2.max_tokens)
```

Output:

```text
50
200
```

Both objects use the same class, but their instance attributes contain different values.

### Modify one instance

```python
config1.max_tokens = 75

print(config1.max_tokens)
print(config2.max_tokens)
```

Output:

```text
75
200
```

Changing `config1.max_tokens` does not change `config2.max_tokens`, because each object stores its own instance attribute.

## 9. Common Mistakes

### Mistake 1: Forgetting `self` in `__init__()`

Incorrect:

```python
class Dog:
    def __init__(name):
        name = name
```

This does not define the initializer correctly for normal instance initialization. Python passes the new instance automatically, so the method needs a parameter to receive it.

Correct:

```python
class Dog:
    def __init__(self, name):
        self.name = name
```

### Mistake 2: Forgetting `self` when storing an attribute

Incorrect:

```python
class Dog:
    def __init__(self, name):
        name = name
```

This assignment does not store the value on the object.

Correct:

```python
class Dog:
    def __init__(self, name):
        self.name = name
```

Now you can access the attribute using `dog.name`.

### Mistake 3: Forgetting parentheses when creating an instance

Incorrect:

```python
class Dog:
    pass


dog1 = Dog
```

Here, `dog1` refers to the class itself, not an instance.

Correct:

```python
dog1 = Dog()
```

Parentheses call the class to create an instance.

### Mistake 4: Confusing instance attributes with class attributes

Consider:

```python
class Dog:
    species = "Canine"

    def __init__(self, name):
        self.name = name


dog1 = Dog("Buddy")
dog2 = Dog("Max")

print(dog1.species)
print(dog2.species)
```

Output:

```text
Canine
Canine
```

Here, `species` is a class attribute shared through the class, while `name` is an instance attribute.

For now, focus on using `self.attribute` for information that belongs to an individual object. You will explore class attributes in more detail later.

## 10. Practice Exercises

Try these exercises before checking the solutions.

### Exercise 1: Create a `Student` class

Create a class named `Student` with these attributes:

- `name`
- `age`
- `course`

Create two student objects and print their details.

### Exercise 2: Create a `Server` class

Create a class named `Server` that stores:

- `hostname`
- `ip_address`
- `environment`

Create an object representing a development server and print its attributes.

### Exercise 3: Use default parameters

Create a class named `Product` with:

- `name`
- `price`
- `currency`, with a default value of `"INR"`

Create one product using the default currency and another with `"USD"`.

### Exercise 4: Modify an instance attribute

Create two `Student` objects. Change the course of the first student and verify that the second student's course remains unchanged.

## 11. Exercise Solutions

### Solution 1: Student

```python
class Student:
    def __init__(self, name, age, course):
        self.name = name
        self.age = age
        self.course = course


student1 = Student("Arun", 21, "Python")
student2 = Student("Priya", 22, "AI Engineering")

print(student1.name, student1.age, student1.course)
print(student2.name, student2.age, student2.course)
```

### Solution 2: Server

```python
class Server:
    def __init__(self, hostname, ip_address, environment):
        self.hostname = hostname
        self.ip_address = ip_address
        self.environment = environment


server = Server("web-dev-01", "192.168.1.10", "development")

print(server.hostname)
print(server.ip_address)
print(server.environment)
```

### Solution 3: Product

```python
class Product:
    def __init__(self, name, price, currency="INR"):
        self.name = name
        self.price = price
        self.currency = currency


product1 = Product("Keyboard", 1500)
product2 = Product("Monitor", 250, currency="USD")

print(product1.name, product1.price, product1.currency)
print(product2.name, product2.price, product2.currency)
```

### Solution 4: Modify an instance attribute

```python
class Student:
    def __init__(self, name, course):
        self.name = name
        self.course = course


student1 = Student("Arun", "Python")
student2 = Student("Priya", "Linux")

student1.course = "AI Engineering"

print(student1.course)
print(student2.course)
```

Output:

```text
AI Engineering
Linux
```

## 12. Summary

In this lesson, you learned how to:

- Define a class using `class`.
- Initialize objects using `__init__()`.
- Use `self` to store and access instance attributes.
- Create objects using positional and keyword arguments.
- Use default parameter values.
- Distinguish between a class and its instances.
- Modify one object's attributes independently of another object's attributes.

**Key takeaway:** A class defines a structure, while each instance stores its own object-specific data.

## 13. What's Next?

In the next lesson, **Methods and Attributes**, you will learn how to add behavior to classes, create methods that return values, and let objects perform useful operations using their own data.
