# Python Methods and Attributes — Add Functionality to Classes

## 1. Introduction

In the previous lesson, you learned how to create classes and initialize objects using `__init__()`.

Now, let's learn how to make objects more useful by adding **attributes and methods**.

By the end of this lesson, you will understand:

- Instance attributes and class attributes.
- How to define and call methods.
- How methods access and modify object data.
- How to track information separately for each object.
- Common mistakes involving class attributes and initialization.

## 2. Attributes — Storing Data

An attribute is a value associated with an object or a class.

For example, an API client might store its API key, server URL, request count, and software version.

Python commonly uses two types of attributes:

1. **Instance attributes:** Store data associated with an individual object.
2. **Class attributes:** Store data associated with the class and commonly shared by its instances.

### 2.1 Instance attributes

Instance attributes belong to individual objects. Different objects can store different values.

Example:

```python
class APIClient:
    def __init__(self, api_key, base_url):
        self.api_key = api_key
        self.base_url = base_url
        self.request_count = 0


client1 = APIClient(
    api_key="key-placeholder-1",
    base_url="https://api1.example.com"
)

client2 = APIClient(
    api_key="key-placeholder-2",
    base_url="https://api2.example.com"
)

print(client1.base_url)
print(client2.base_url)
print(client1.request_count)
```

Output:

```text
https://api1.example.com
https://api2.example.com
0
```

Let's understand the attributes:

- `self.api_key` stores the key associated with that client.
- `self.base_url` stores the client's base URL.
- `self.request_count` tracks the number of requests made by that client.

Each object maintains its own instance attributes.

For example, changing the request count of `client1` does not change the request count of `client2`.

```python
client1.request_count = 5

print(client1.request_count)
print(client2.request_count)
```

Output:

```text
5
0
```

This separation is useful when managing multiple API clients, servers, users, or other independent objects.

### 2.2 Class attributes

Class attributes are defined directly inside the class body, outside instance methods.

They are useful for values that should be associated with the class and shared by its instances.

Example:

```python
class APIClient:
    version = "1.0"
    max_retries = 3

    def __init__(self, api_key):
        self.api_key = api_key


client1 = APIClient("key-placeholder-1")
client2 = APIClient("key-placeholder-2")

print(client1.version)
print(client2.version)
print(APIClient.max_retries)
```

Output:

```text
1.0
1.0
3
```

Here:

- `version` is a class attribute.
- `max_retries` is a class attribute.
- `api_key` is an instance attribute.

You can access class attributes through the class itself or through an instance.

```python
print(APIClient.version)
print(client1.version)
```

Both expressions return `"1.0"`.

### 2.3 Instance attributes versus class attributes

| Feature | Instance attribute | Class attribute |
|---|---|---|
| Defined | Commonly inside `__init__()` using `self` | Directly inside the class body |
| Associated with | An individual instance | The class |
| Typical use | API key, hostname, username | Default version, shared configuration |
| Access | `client1.api_key` | `APIClient.version` |

**Important:** A class attribute is not automatically immutable. If you change it through the class, instances that do not override that attribute will generally see the updated value.

```python
class APIClient:
    version = "1.0"


client1 = APIClient()
client2 = APIClient()

APIClient.version = "2.0"

print(client1.version)
print(client2.version)
```

Output:

```text
2.0
2.0
```

However, assigning through an instance creates or updates an instance attribute, which can hide the class attribute for that object.

```python
client1.version = "custom"

print(client1.version)
print(client2.version)
print(APIClient.version)
```

Output:

```text
custom
2.0
2.0
```

For this reason, use `ClassName.attribute` when you intend to update a shared class-level setting.

## 3. Methods — Adding Behavior

A method is a function defined inside a class.

Methods allow objects to perform operations using their attributes.

For example, an API client might have methods to:

- Send a request.
- Track the number of requests.
- Reset its request counter.
- Display its configuration.

Let's create a simple class with methods.

```python
class APIClient:
    def __init__(self, base_url):
        self.base_url = base_url
        self.request_count = 0

    def record_request(self):
        self.request_count += 1

    def display_status(self):
        print(f"API URL: {self.base_url}")
        print(f"Requests: {self.request_count}")


client = APIClient("https://api.example.com")

client.record_request()
client.record_request()

client.display_status()
```

Output:

```text
API URL: https://api.example.com
Requests: 2
```

### Understanding the methods

The method:

```python
def record_request(self):
    self.request_count += 1
```

increases the current object's request counter by one.

The method:

```python
def display_status(self):
    print(f"API URL: {self.base_url}")
    print(f"Requests: {self.request_count}")
```

uses the current object's attributes to display its status.

When you call:

```python
client.record_request()
```

Python automatically passes `client` as the first argument, `self`.

You do not need to write:

```python
client.record_request(client)
```

That would pass an extra argument and cause an error.

## 4. Methods with Parameters and Return Values

Methods can accept parameters and return results, just like regular functions.

Let's build a data validator.

```python
class DataValidator:
    def __init__(self):
        self.errors = []

    def validate_email(self, email):
        if "@" not in email:
            self.errors.append(f"Invalid email: {email}")
            return False

        return True

    def validate_age(self, age):
        if not isinstance(age, int) or isinstance(age, bool):
            self.errors.append(f"Age must be an integer: {age}")
            return False

        if age < 0 or age > 150:
            self.errors.append(f"Invalid age: {age}")
            return False

        return True

    def get_errors(self):
        return self.errors


validator = DataValidator()

print(validator.validate_email("bad-email"))
print(validator.validate_age(200))
print(validator.validate_email("user@example.com"))

print(validator.get_errors())
```

Output:

```text
False
False
True
['Invalid email: bad-email', 'Invalid age: 200']
```

### Understanding the code

- `self.errors = []` initializes a separate error list for each validator object.
- `validate_email()` checks whether the supplied text contains `@`. This is a basic demonstration, not comprehensive email validation.
- `validate_age()` checks the type and range of the supplied age.
- `get_errors()` returns the errors collected by the object.

Notice that `get_errors()` returns a list. It does not print the list itself; the `print()` call displays the returned value.

### Positional and keyword arguments

You can call the methods using positional arguments:

```python
validator.validate_email("user@example.com")
```

Or keyword arguments:

```python
validator.validate_email(email="user@example.com")
```

Both calls pass the email value to the method.

## 5. Methods That Modify Object State

An object's *state* is the data it currently stores.

A method can change that state by updating instance attributes.

Let's create a simple server monitor.

```python
class Server:
    def __init__(self, hostname, cpu_usage=0):
        self.hostname = hostname
        self.cpu_usage = cpu_usage

    def update_cpu_usage(self, usage):
        if not isinstance(usage, (int, float)) or isinstance(usage, bool):
            raise TypeError("CPU usage must be a number.")

        if not 0 <= usage <= 100:
            raise ValueError("CPU usage must be between 0 and 100.")

        self.cpu_usage = usage

    def check_health(self):
        if self.cpu_usage >= 90:
            return "WARNING"
        return "OK"


server = Server("web-01", 65)

print(server.check_health())

server.update_cpu_usage(95)

print(server.check_health())
```

Output:

```text
OK
WARNING
```

The `update_cpu_usage()` method validates the input before changing the object's state.

The `check_health()` method reads the current CPU usage and returns a status.

This illustrates an important OOP principle: methods can encapsulate the logic for safely working with an object's data.

## 6. Common Mistakes

### Mistake 1: Modifying a mutable class attribute

Lists and dictionaries are mutable. If you define a list as a class attribute, all instances that use that list share the same object.

Incorrect:

```python
class DataValidator:
    errors = []

    def add_error(self, message):
        self.errors.append(message)


validator1 = DataValidator()
validator2 = DataValidator()

validator1.add_error("Invalid email")

print(validator2.errors)
```

Output:

```text
['Invalid email']
```

The second validator unexpectedly sees the first validator's error because both use the same class-level list.

Correct:

```python
class DataValidator:
    def __init__(self):
        self.errors = []

    def add_error(self, message):
        self.errors.append(message)


validator1 = DataValidator()
validator2 = DataValidator()

validator1.add_error("Invalid email")

print(validator1.errors)
print(validator2.errors)
```

Output:

```text
['Invalid email']
[]
```

**Rule:** Initialize mutable instance data, such as lists and dictionaries, inside `__init__()` when each object needs its own copy.

### Mistake 2: Not initializing an attribute

Incorrect:

```python
class APIClient:
    def display_status(self):
        print(self.request_count)


client = APIClient()
client.display_status()
```

This raises `AttributeError` because `request_count` has not been defined on the object.

Correct:

```python
class APIClient:
    def __init__(self):
        self.request_count = 0

    def display_status(self):
        print(self.request_count)


client = APIClient()
client.display_status()
```

Output:

```text
0
```

Initialize the attributes your methods require before using them.

### Mistake 3: Forgetting `self` in a method

Incorrect:

```python
class Calculator:
    def add(a, b):
        return a + b


calculator = Calculator()
calculator.add(10, 20)
```

This raises `TypeError` because Python automatically passes the instance to the method, but the method does not have a separate parameter for it.

Correct:

```python
class Calculator:
    def add(self, a, b):
        return a + b


calculator = Calculator()

print(calculator.add(10, 20))
```

Output:

```text
30
```

### Mistake 4: Forgetting to return a value

Incorrect:

```python
class Calculator:
    def add(self, a, b):
        result = a + b


calculator = Calculator()

print(calculator.add(10, 20))
```

Output:

```text
None
```

The method calculates the result but never returns it.

Correct:

```python
class Calculator:
    def add(self, a, b):
        return a + b


calculator = Calculator()

print(calculator.add(10, 20))
```

Output:

```text
30
```

Remember that `return` sends a value back to the caller, while `print()` only displays a value.

## 7. Practice Exercises

Try these exercises before checking the solutions.

### Exercise 1: Create a counter

Create a class named `Counter` with an instance attribute named `count`, initially set to `0`.

Add methods to:
- Increase the count by one.
- Reset the count to zero.
- Display the current count.

### Exercise 2: Create a temperature converter

Create a class named `TemperatureConverter` with a method called `celsius_to_fahrenheit()`.

Use this formula:

\[
F = \frac{9}{5}C + 32
\]

Expected output for 25°C:

```text
77.0
```

### Exercise 3: Track API requests

Create an `APIClient` class that stores:
- `base_url`
- `request_count`, initially set to zero

Add a method called `record_request()` that increases the request count.

Create two clients and verify that their counters are independent.

### Exercise 4: Validate server CPU usage

Create a `Server` class with a hostname and CPU usage.

Add a method called `check_health()` that returns:
- `"OK"` when CPU usage is below 90%.
- `"WARNING"` when CPU usage is at least 90%.

Add basic validation to reject CPU values outside the range of 0–100.

## 8. Exercise Solutions

### Solution 1: Counter

```python
class Counter:
    def __init__(self):
        self.count = 0

    def increment(self):
        self.count += 1

    def reset(self):
        self.count = 0

    def display(self):
        print(self.count)


counter = Counter()

counter.increment()
counter.increment()
counter.display()

counter.reset()
counter.display()
```

Output:

```text
2
0
```

### Solution 2: Temperature converter

```python
class TemperatureConverter:
    def celsius_to_fahrenheit(self, celsius):
        return (9 / 5) * celsius + 32


converter = TemperatureConverter()

print(converter.celsius_to_fahrenheit(25))
```

Output:

```text
77.0
```

### Solution 3: API request counter

```python
class APIClient:
    def __init__(self, base_url):
        self.base_url = base_url
        self.request_count = 0

    def record_request(self):
        self.request_count += 1


client1 = APIClient("https://api1.example.com")
client2 = APIClient("https://api2.example.com")

client1.record_request()
client1.record_request()
client2.record_request()

print(client1.request_count)
print(client2.request_count)
```

Output:

```text
2
1
```

### Solution 4: Server health checker

```python
class Server:
    def __init__(self, hostname, cpu_usage):
        self.hostname = hostname
        self.set_cpu_usage(cpu_usage)

    def set_cpu_usage(self, usage):
        if not isinstance(usage, (int, float)) or isinstance(usage, bool):
            raise TypeError("CPU usage must be a number.")

        if not 0 <= usage <= 100:
            raise ValueError("CPU usage must be between 0 and 100.")

        self.cpu_usage = usage

    def check_health(self):
        if self.cpu_usage >= 90:
            return "WARNING"
        return "OK"


server1 = Server("web-01", 65)
server2 = Server("web-02", 95)

print(server1.check_health())
print(server2.check_health())
```

Output:

```text
OK
WARNING
```

## 9. Summary

In this lesson, you learned:

- **Instance attributes** store data specific to each object.
- **Class attributes** are associated with the class and can be shared by its instances.
- **Methods** define the behavior of objects.
- `self` refers to the current instance.
- Methods can read attributes, modify state, accept parameters, and return results.
- Mutable class attributes can unintentionally share data between objects.
- Attributes should be initialized before methods depend on them.

## 10. What's Next?

Next, you will learn about **Inheritance** — how one Python class can reuse and extend the functionality of another class.
