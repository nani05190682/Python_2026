# Python Classes — Create Your Own Data Types

## 1. Introduction to Object-Oriented Programming (OOP)

Object-oriented programming (OOP) is a programming approach that organizes code by grouping related data and functions into objects.

As you learned earlier, variables store data and functions perform operations. As a program grows, managing many separate variables and functions can become difficult.

OOP helps you organize related information and behavior into a single structure.

### A real-world example

Think about a car.

A car has data:
- Brand
- Model
- Color
- Speed

A car can also perform actions:
- Start
- Accelerate
- Brake
- Stop

In Python, we can represent a car as an object that contains both its data and its behavior.

### Without classes

```python
car_brand = "Mahindra"
car_model = "XUV 7XO"
car_speed = 0

def accelerate(speed, amount):
    return speed + amount

car_speed = accelerate(car_speed, 20)

print(car_brand)
print(car_model)
print(car_speed)
```

Output:

```text
Mahindra
XUV 7XO
20
```

This works, but managing many cars would require keeping track of separate variables and passing the correct values to functions.

### With classes

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
        self.speed = 0

    def accelerate(self, amount):
        self.speed += amount

    def display_info(self):
        print(f"Brand: {self.brand}")
        print(f"Model: {self.model}")
        print(f"Speed: {self.speed} km/h")


car = Car("Mahindra", "XUV 7XO")

car.accelerate(20)
car.display_info()
```

Output:

```text
Brand: Mahindra
Model: XUV 7XO
Speed: 20 km/h
```

Here, the car's information and actions are grouped together.

**Important:** You do not need classes for every Python program. Functions and simple data structures are often sufficient. Classes become useful when you need to represent objects that combine related data and behavior.

## 2. What Is a Class?

A **class** is a blueprint for creating objects.

An **object** is an instance of a class.

Consider a house blueprint. The blueprint defines the structure of a house, but you can build multiple houses from that same blueprint.

Similarly, a Python class defines the structure and behavior of objects, and you can create multiple objects from one class.

<text>**Blueprint versus objects**</text>

| Concept | Python example | Meaning |
|---|---|---|
| Class | `Car` | Blueprint |
| Object | `car1` | One car created from the blueprint |
| Object | `car2` | Another car created from the same blueprint |
| Attribute | `car1.brand` | Data stored by an object |
| Method | `car1.accelerate(20)` | Action performed by an object |

### Your first class

```python
class Student:
    pass
```

Let's understand the code:

- `class` is the keyword used to define a class.
- `Student` is the class name.
- `pass` is a placeholder that allows the class body to remain empty temporarily.

Create an object:

```python
student1 = Student()

print(student1)
```

Python creates a `Student` object and assigns a reference to it to the variable `student1`.

The displayed object representation includes implementation-specific details, so your output will look similar to:

```text
<__main__.Student object at 0x...>
```

The memory address-like portion can differ between runs.

## 3. Your First Practical Class

Let's create a class that represents a student.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student1 = Student("Arun", 21)
student2 = Student("Priya", 22)

print(student1.name)
print(student1.age)

print(student2.name)
print(student2.age)
```

Output:

```text
Arun
21
Priya
22
```

### Understanding `__init__()`

The `__init__()` method initializes an object when you create it.

```python
def __init__(self, name, age):
```

When Python executes:

```python
student1 = Student("Arun", 21)
```

Python creates a new `Student` object and calls its initialization method with the new object, `"Arun"`, and `21`.

Inside the method:

```python
self.name = name
self.age = age
```

The values are stored as attributes of that particular object.

### What is `self`?

`self` refers to the current instance of the class.

For example:

```python
student1 = Student("Arun", 21)
student2 = Student("Priya", 22)
```

- `student1.name` is `"Arun"`.
- `student2.name` is `"Priya"`.

Each object has its own instance attributes.

**Remember:** `self` is a conventional parameter name, not a Python keyword. Use it as the first parameter of ordinary instance methods.

## 4. Attributes and Methods

Classes commonly contain two important elements.

### Attributes

Attributes store information about an object.

Examples:

```python
student1.name
student1.age
```

These are instance attributes.

### Methods

Methods are functions defined inside a class that typically operate on its objects.

Let's add a method to our `Student` class.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print(f"My name is {self.name}.")
        print(f"I am {self.age} years old.")


student = Student("Arun", 21)

student.introduce()
```

Output:

```text
My name is Arun.
I am 21 years old.
```

Notice how the method accesses the object's attributes using `self`.

You call the method using:

```python
student.introduce()
```

Python automatically passes `student` as the instance argument to this ordinary method. You do not write `student.introduce(student)`.

## 5. Adding Functionality to Classes

Let's create a class for monitoring a server, a practical example in DevOps and SRE.

```python
class Server:
    def __init__(self, hostname, cpu_usage):
        self.hostname = hostname
        self.cpu_usage = cpu_usage

    def update_cpu_usage(self, usage):
        if 0 <= usage <= 100:
            self.cpu_usage = usage
        else:
            print("CPU usage must be between 0 and 100.")

    def check_health(self):
        if self.cpu_usage >= 90:
            print(f"WARNING: {self.hostname} has high CPU usage.")
        else:
            print(f"OK: {self.hostname} is healthy.")

    def display_status(self):
        print(f"Hostname: {self.hostname}")
        print(f"CPU Usage: {self.cpu_usage}%")


server = Server("web-01", 65)

server.display_status()
server.check_health()

server.update_cpu_usage(95)
server.check_health()
```

Output:

```text
Hostname: web-01
CPU Usage: 65%
OK: web-01 is healthy.
WARNING: web-01 has high CPU usage.
```

### What did we learn?

The `Server` class groups related data and operations together:

- `hostname` stores the server name.
- `cpu_usage` stores CPU utilization.
- `update_cpu_usage()` updates the utilization after basic validation.
- `check_health()` evaluates the utilization against a threshold.
- `display_status()` displays the current status.

This example demonstrates how a class can represent a real-world entity and its behavior.

In a real monitoring system, CPU usage would normally come from a monitoring API or operating-system metrics rather than a manually supplied value.

## 6. Inheritance — Build on Existing Classes

**Inheritance** allows one class to reuse and extend functionality defined by another class.

For example, you might have a general `Server` class and specialized classes for web servers and database servers.

### Example

```python
class Server:
    def __init__(self, hostname):
        self.hostname = hostname

    def show_hostname(self):
        print(f"Hostname: {self.hostname}")


class WebServer(Server):
    def deploy_application(self):
        print(f"Deploying application on {self.hostname}")


class DatabaseServer(Server):
    def backup_database(self):
        print(f"Backing up database on {self.hostname}")


web = WebServer("web-01")
database = DatabaseServer("db-01")

web.show_hostname()
web.deploy_application()

database.show_hostname()
database.backup_database()
```

Output:

```text
Hostname: web-01
Deploying application on web-01
Hostname: db-01
Backing up database on db-01
```

### Understanding the example

- `Server` is the parent class, also called the base class.
- `WebServer` and `DatabaseServer` are child classes, also called derived classes.
- Both child classes inherit `show_hostname()` from `Server`.
- Each child class defines its own specialized method.

The syntax:

```python
class WebServer(Server):
```

means that `WebServer` inherits from `Server`.

### When should you use inheritance?

Use inheritance when classes share a meaningful common type and the child classes need to specialize the parent's behavior.

Do not use inheritance simply to avoid repeating a few lines of code. Sometimes, composing objects from smaller components is a better design.

## 7. When Should You Use Classes?

Classes are especially useful when your program needs to manage multiple related objects, maintain state, or provide a reusable interface.

| Scenario | Possible class |
|---|---|
| Calling an AI API | `AIClient` |
| Managing servers | `Server` |
| Processing datasets | `DataProcessor` |
| Managing cloud resources | `CloudResource` |
| Representing a user | `User` |
| Managing database connections | `DatabaseClient` |

### Example: An AI client

A class can store API configuration and provide a method for generating responses.

```python
class AIClient:
    def __init__(self, model):
        self.model = model

    def generate(self, prompt):
        print(f"Model: {self.model}")
        print(f"Prompt: {prompt}")


client = AIClient("example-model")

client.generate("Explain Python classes.")
```

Output:

```text
Model: example-model
Prompt: Explain Python classes.
```

This is a simplified example, not a real API integration. A production AI client would also need API authentication, HTTP requests, timeout handling, error handling, and secure management of credentials.

## 8. Best Practices for Classes

1. **Use descriptive names.** Choose `Server`, `Student`, or `AIClient` instead of vague names such as `Thing`.
2. **Follow naming conventions.** Class names generally use `PascalCase`, such as `DatabaseClient`. Methods and attributes generally use `snake_case`, such as `check_health`.
3. **Keep each class focused.** A class should have a clear responsibility.
4. **Use instance attributes for object-specific data.** Store each object's hostname, name, or configuration on that instance.
5. **Avoid unnecessary classes.** A small script or a simple calculation may be easier to express with functions.
6. **Reuse code thoughtfully.** Consider functions, composition, and inheritance when appropriate.
7. **Avoid hardcoding secrets.** Never place real API keys or passwords directly in source code.
8. **Test class behavior.** Check normal operation, invalid inputs, and expected edge cases.

## 9. Practice Exercises

Try these exercises before looking at the solutions.

### Exercise 1: Create a `Book` class

Create a class named `Book` with these attributes:

- `title`
- `author`
- `price`

Create two book objects and print their information.

### Exercise 2: Add a method

Create a `Rectangle` class with `length` and `width` attributes.

Add a method named `calculate_area()` that returns the rectangle's area.

Expected behavior:

```python
rectangle = Rectangle(10, 5)
print(rectangle.calculate_area())
```

Output:

```text
50
```

### Exercise 3: Create a server monitor

Create a `Server` class with:

- `hostname`
- `cpu_usage`
- A method named `check_health()`

The method should print a warning if CPU usage is at least 90%; otherwise, it should report normal CPU usage.

### Exercise 4: Practice inheritance

Create a parent class named `Employee` with a `name` attribute and a `show_name()` method.

Create a child class named `Developer` that inherits from `Employee` and adds a `write_code()` method.

## 10. Exercise Solutions

### Solution 1: Book

```python
class Book:
    def __init__(self, title, author, price):
        self.title = title
        self.author = author
        self.price = price

    def display_info(self):
        print(f"Title: {self.title}")
        print(f"Author: {self.author}")
        print(f"Price: ₹{self.price}")


book1 = Book("Python Basics", "Arun", 500)
book2 = Book("AI Engineering", "Priya", 750)

book1.display_info()
book2.display_info()
```

### Solution 2: Rectangle

```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def calculate_area(self):
        return self.length * self.width


rectangle = Rectangle(10, 5)

print(rectangle.calculate_area())
```

Output:

```text
50
```

### Solution 3: Server monitor

```python
class Server:
    def __init__(self, hostname, cpu_usage):
        self.hostname = hostname
        self.cpu_usage = cpu_usage

    def check_health(self):
        if self.cpu_usage >= 90:
            print(f"WARNING: High CPU usage on {self.hostname}")
        else:
            print(f"OK: {self.hostname} is operating normally.")


server1 = Server("web-01", 75)
server2 = Server("web-02", 95)

server1.check_health()
server2.check_health()
```

Output:

```text
OK: web-01 is operating normally.
WARNING: High CPU usage on web-02
```

### Solution 4: Inheritance

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def show_name(self):
        print(f"Employee: {self.name}")


class Developer(Employee):
    def write_code(self):
        print(f"{self.name} is writing code.")


developer = Developer("Arun")

developer.show_name()
developer.write_code()
```

Output:

```text
Employee: Arun
Arun is writing code.
```

## 11. Summary

In this lesson, you learned:

- **OOP:** A way to organize related data and behavior.
- **Class:** A blueprint for creating objects.
- **Object:** An instance of a class.
- **Attribute:** Data associated with an object.
- **Method:** A function defined inside a class.
- **`__init__()`:** Initializes a newly created object.
- **`self`:** Refers to the current instance.
- **Inheritance:** Allows a class to reuse and extend another class's functionality.

The most important concept to remember is that a class defines how objects are structured, while each object represents a particular instance with its own data.

## 12. What's Next?

Next, learn more about **Python Objects, Attributes, and Methods**. You will explore instance attributes, class attributes, instance methods, and how different objects maintain their own state.
