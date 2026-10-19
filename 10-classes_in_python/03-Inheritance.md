# Python Inheritance — Build on Existing Classes

## 1. Introduction

In the previous lessons, you learned how to create classes, initialize objects, define attributes, and add methods.

Now, let's explore **inheritance**, a feature of object-oriented programming (OOP) that allows one class to reuse and extend another class's functionality.

Inheritance becomes useful when your application contains multiple related types of objects that share common behavior.

For example, a cloud management application might manage virtual machines, containers, and storage resources. These resources may share common attributes, such as a name and status, while each type has its own specialized operations.

By the end of this lesson, you will understand:

- What inheritance is and why it is useful.
- The difference between parent and child classes.
- How to inherit attributes and methods.
- How to use `super()` to initialize parent attributes.
- How to override inherited methods.
- When inheritance is appropriate and when to avoid it.

## 2. What Is Inheritance?

**Inheritance allows you to create a new class based on an existing class.**

The new class can reuse the existing class's functionality and add its own attributes and methods.

Inheritance introduces two important terms:

- **Parent class:** The class whose functionality is inherited.
- **Child class:** The class that inherits from the parent class.

Think about the relationship between animals and dogs.

- An animal can eat and sleep.
- A dog can eat and sleep.
- A dog can also bark.

Instead of implementing eating and sleeping separately for every animal type, you can define those behaviors once in a parent class.

<text>**Inheritance structure**</text>

<box border radius="lg" padding={3} gap={2} align="center">
  <box background="surface-secondary" radius="md" padding={3} width="75%" align="center">
    **Animal**

    <text size="sm">Common attributes and methods</text>
    <text size="sm" color="secondary">name · eat() · sleep()</text>
  </box>
  <icon name="arrow-down" size="xl" color="secondary" />
  <box background="surface" border radius="md" padding={3} width="75%" align="center">
    **Dog**

    <text size="sm">Inherits Animal behavior</text>
    <text size="sm" color="secondary">Adds bark()</text>
  </box>
</box>

## 3. Your First Inheritance Example

Let's create a parent class named `Animal` and a child class named `Dog`.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        return f"{self.name} is eating"

    def sleep(self):
        return f"{self.name} is sleeping"


class Dog(Animal):
    def bark(self):
        return f"{self.name} says woof!"


my_dog = Dog("Buddy")

print(my_dog.eat())
print(my_dog.sleep())
print(my_dog.bark())
```

Output:

```text
Buddy is eating
Buddy is sleeping
Buddy says woof!
```

### Understanding the code

**Step 1: Create the parent class**

```python
class Animal:
    def __init__(self, name):
        self.name = name
```

The `Animal` class stores the animal's name.

It also defines the `eat()` and `sleep()` methods.

**Step 2: Create the child class**

```python
class Dog(Animal):
```

The expression `(Animal)` tells Python that `Dog` inherits from `Animal`.

The `Dog` class can use the parent's methods without defining them again.

**Step 3: Add a specialized method**

```python
def bark(self):
    return f"{self.name} says woof!"
```

The `Dog` class defines its own `bark()` method.

**Step 4: Create an object**

```python
my_dog = Dog("Buddy")
```

Python uses the inherited initializer to initialize the `Dog` object's name.

The object can then use both inherited methods and its own method.

```python
my_dog.eat()
my_dog.sleep()
my_dog.bark()
```

Notice that you do not need to pass `self` when calling these methods.

## 4. Adding Attributes to Child Classes

A child class can have additional attributes that do not exist in the parent class.

For example, all animals have a name, but dogs also have a breed.

We can use `super()` to initialize the parent portion of the object.

```python
class Animal:
    def __init__(self, name):
        self.name = name
        self.is_pet = True


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed

    def describe(self):
        return f"{self.name} is a {self.breed}"


golden = Dog("Buddy", "Golden Retriever")
poodle = Dog(name="Max", breed="Poodle")

print(golden.describe())
print(golden.is_pet)
print(poodle.describe())
```

Output:

```text
Buddy is a Golden Retriever
True
Max is a Poodle
```

### What does `super()` do?

The line:

```python
super().__init__(name)
```

calls the parent class's initializer through Python's method resolution system.

This allows the parent class to initialize attributes such as `name` and `is_pet`.

The child class then initializes its own attribute:

```python
self.breed = breed
```

Without the parent initialization call, the child's initializer would need to set up the inherited attributes itself.

**Remember:** When a child class defines its own `__init__()`, Python does not automatically call the parent's `__init__()`. If parent initialization is required, explicitly call `super().__init__(...)`.

## 5. Method Overriding

A child class can provide its own implementation of a method inherited from its parent. This is called **method overriding**.

For example, different animals make different sounds.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        return f"{self.name} makes a sound"


class Dog(Animal):
    def make_sound(self):
        return f"{self.name} barks: Woof!"


class Cat(Animal):
    def make_sound(self):
        return f"{self.name} meows: Meow!"


generic = Animal("Animal")
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(generic.make_sound())
print(dog.make_sound())
print(cat.make_sound())
```

Output:

```text
Animal makes a sound
Buddy barks: Woof!
Whiskers meows: Meow!
```

### What happens here?

The parent class defines a general implementation:

```python
def make_sound(self):
    return f"{self.name} makes a sound"
```

The child classes replace that behavior with specialized implementations.

When you call:

```python
dog.make_sound()
```

Python finds the method defined in `Dog` and uses it instead of the parent's version.

Similarly, `cat.make_sound()` calls the implementation defined in `Cat`.

This is one of the key benefits of inheritance: related classes can share a common interface while behaving differently.

## 6. Using `super()` to Extend a Parent Method

Sometimes you do not want to replace the parent's behavior completely. You may want to reuse it and then add extra functionality.

For example:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def describe(self):
        return f"Animal name: {self.name}"


class Dog(Animal):
    def describe(self):
        parent_description = super().describe()
        return f"{parent_description}. This animal is a dog."


dog = Dog("Buddy")

print(dog.describe())
```

Output:

```text
Animal name: Buddy. This animal is a dog.
```

Here, `super().describe()` calls the parent's method. The child class then extends the returned description.

Use this approach when you want to preserve useful parent behavior rather than duplicate it.

## 7. Real-World Example — AI Model Classes

Inheritance can help organize AI components that share common functionality.

Let's create a base class called `BaseModel` and a specialized class called `TextModel`.

```python
class BaseModel:
    def __init__(self, model_name):
        self.model_name = model_name
        self.is_loaded = False

    def load(self):
        print(f"Loading {self.model_name}...")
        self.is_loaded = True


class TextModel(BaseModel):
    def __init__(self, model_name, max_length=1000):
        super().__init__(model_name)
        self.max_length = max_length

    def process_text(self, text):
        if not self.is_loaded:
            self.load()

        if len(text) > self.max_length:
            text = text[:self.max_length]

        return f"Processed: {text}"


model = TextModel(
    model_name="example-text-model",
    max_length=100
)

result = model.process_text("Hello world")

print(result)
print(model.is_loaded)
```

Output:

```text
Loading example-text-model...
Processed: Hello world
True
```

### Understanding the design

The `BaseModel` class provides shared functionality:

- `model_name` stores the model's name.
- `is_loaded` tracks whether the model has been marked as loaded.
- `load()` updates that state.

The `TextModel` class adds specialized functionality:

- `max_length` stores the maximum permitted text length.
- `process_text()` ensures that the model is marked as loaded and truncates the text if necessary.

This is a simplified demonstration. The `load()` method does not download or initialize an actual AI model, and `process_text()` does not perform inference.

In a real AI application, a base class might define a common interface for loading models and processing inputs, while child classes implement model-specific operations.

## 8. When Should You Use Inheritance?

Inheritance is useful when classes have a genuine **"is-a" relationship** and share behavior that belongs in a common parent.

### Good examples

| Parent class | Child class | Relationship |
|---|---|---|
| `Animal` | `Dog` | A dog is an animal |
| `Employee` | `Developer` | A developer is an employee |
| `BaseModel` | `TextModel` | A text model is a type of model |
| `CloudResource` | `VirtualMachine` | A virtual machine is a type of cloud resource |

### When to avoid inheritance

Avoid inheritance when:

- The classes are only loosely related.
- You want to reuse just one small function.
- The child class does not meaningfully represent a type of the parent.
- The inheritance hierarchy becomes difficult to understand.
- The child class must override nearly every parent method.

In these situations, standalone functions or **composition** may be better choices. Composition means building an object using other objects rather than inheriting all their behavior.

For example, an `AIClient` that uses a `Logger` can simply hold a reference to a logger object. It does not need to inherit from `Logger`.

## 9. Common Mistakes

### Mistake 1: Forgetting `super().__init__()`

Incorrect:

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        self.breed = breed


dog = Dog("Buddy", "Beagle")
print(dog.name)
```

This raises `AttributeError` because the child initializer did not initialize `self.name`.

Correct:

```python
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

Now the parent initializer sets up `name`, and the child initializer sets up `breed`.

### Mistake 2: Choosing the wrong inheritance relationship

Suppose you define:

```python
class Engine:
    pass


class Car(Engine):
    pass
```

This design implies that a car *is an* engine, which is not correct.

A car has an engine, so composition is more appropriate:

```python
class Engine:
    def start(self):
        return "Engine started"


class Car:
    def __init__(self):
        self.engine = Engine()


car = Car()

print(car.engine.start())
```

Output:

```text
Engine started
```

The `Car` object contains an `Engine` object instead of inheriting from it.

### Mistake 3: Repeating parent functionality

If a parent class already defines a useful method, avoid copying the same implementation into every child class unless the behavior genuinely needs to change.

Instead, inherit the method or extend it using `super()`.

## 10. Practice Exercises

Try solving these exercises before checking the solutions.

### Exercise 1: Employee inheritance

Create a parent class named `Employee` with:

- A `name` attribute.
- A `show_details()` method.

Create a child class named `Developer` that adds a `programming_language` attribute.

The developer should be able to display both the employee's name and programming language.

### Exercise 2: Method overriding

Create a parent class named `Notification` with a `send()` method that returns `"Sending notification"`.

Create child classes named `EmailNotification` and `SMSNotification` that override `send()` with their own messages.

### Exercise 3: Cloud resource management

Create a parent class named `CloudResource` with:

- `resource_name`
- `status`
- A `show_status()` method

Create a child class named `VirtualMachine` that adds a `cpu_cores` attribute.

Use `super()` to initialize the parent's attributes.

### Exercise 4: Extend parent behavior

Create a parent class named `Logger` with a method called `log()` that returns a message prefixed with `"LOG:"`.

Create a child class named `ErrorLogger` that uses `super()` and returns a message prefixed with `"ERROR:"`.

## 11. Exercise Solutions

### Solution 1: Employee inheritance

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def show_details(self):
        return f"Employee: {self.name}"


class Developer(Employee):
    def __init__(self, name, programming_language):
        super().__init__(name)
        self.programming_language = programming_language

    def show_details(self):
        return (
            f"Employee: {self.name}, "
            f"Language: {self.programming_language}"
        )


developer = Developer("Arun", "Python")

print(developer.show_details())
```

Output:

```text
Employee: Arun, Language: Python
```

### Solution 2: Method overriding

```python
class Notification:
    def send(self):
        return "Sending notification"


class EmailNotification(Notification):
    def send(self):
        return "Sending email notification"


class SMSNotification(Notification):
    def send(self):
        return "Sending SMS notification"


notifications = [
    EmailNotification(),
    SMSNotification()
]

for notification in notifications:
    print(notification.send())
```

Output:

```text
Sending email notification
Sending SMS notification
```

### Solution 3: Cloud resource management

```python
class CloudResource:
    def __init__(self, resource_name, status):
        self.resource_name = resource_name
        self.status = status

    def show_status(self):
        return f"{self.resource_name}: {self.status}"


class VirtualMachine(CloudResource):
    def __init__(self, resource_name, status, cpu_cores):
        super().__init__(resource_name, status)
        self.cpu_cores = cpu_cores


vm = VirtualMachine("web-vm-01", "Running", 4)

print(vm.show_status())
print(f"CPU cores: {vm.cpu_cores}")
```

Output:

```text
web-vm-01: Running
CPU cores: 4
```

### Solution 4: Extend parent behavior

```python
class Logger:
    def log(self, message):
        return f"LOG: {message}"


class ErrorLogger(Logger):
    def log(self, message):
        parent_message = super().log(message)
        return parent_message.replace("LOG:", "ERROR:", 1)


logger = ErrorLogger()

print(logger.log("Database connection failed"))
```

Output:

```text
ERROR: Database connection failed
```

## 12. Summary

In this lesson, you learned:

- **Inheritance** allows one class to reuse and extend another class.
- A **parent class** defines common functionality.
- A **child class** inherits and can add specialized functionality.
- `super()` allows you to call parent methods, including the parent initializer.
- **Method overriding** lets a child class customize inherited behavior.
- Inheritance is appropriate for genuine "is-a" relationships.
- **Composition** is often better for "has-a" relationships.

The most important takeaway is that inheritance helps you organize related classes, but it should make your code simpler rather than more complicated.

## 13. What's Next?

Next, you will learn **When to Use Classes — Best Practices and Guidelines**. You will explore how to decide between classes, functions, and simple data structures when designing real Python applications.
