# Python OOP — Complete Interview Notes

> **Level:** AI-Powered Full Stack Engineer  
> **Purpose:** Interview revision + practical understanding  
> **Language:** Python

---

## Table of Contents

1. [What is OOP?](#1-what-is-oop)
2. [Class](#2-class)
3. [Object](#3-object)
4. [Attributes](#4-attributes)
5. [Methods](#5-methods)
6. [Constructor `__init__`](#6-constructor-__init__)
7. [`self`](#7-self)
8. [Object Lifecycle](#8-object-lifecycle)
9. [Encapsulation](#9-encapsulation)
10. [Inheritance](#10-inheritance)
11. [Polymorphism](#11-polymorphism)
12. [Abstraction](#12-abstraction)
13. [Class Method](#13-class-method)
14. [Static Method](#14-static-method)
15. [`super()`](#15-super)
16. [Magic / Dunder Methods](#16-magic--dunder-methods)
17. [Composition](#17-composition)
18. [Composition vs Inheritance](#18-composition-vs-inheritance)
19. [SOLID Principles](#19-solid-principles)
20. [Interview Cheat Sheet](#20-interview-cheat-sheet)
21. [Practice Checklist](#21-practice-checklist)

---

# 1. What is OOP?

### Interview Definition

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes software around **objects**, which contain **data (attributes)** and **behavior (methods)**.

### Why use OOP?

- Code reusability
- Modularity
- Maintainability
- Scalability
- Encapsulation
- Better real-world modeling

### Four Core Pillars

```text
Encapsulation
Inheritance
Polymorphism
Abstraction
```

---

# 2. Class

### Definition

A **class** is a blueprint or template for creating objects.

```python
class Student:
    pass
```

### Interview One-Liner

> A class is a blueprint used to create objects.

---

# 3. Object

### Definition

An **object** is an instance of a class.

```python
class Student:
    pass

student1 = Student()
student2 = Student()
```

Here `Student` is the class and `student1`, `student2` are objects.

### Interview One-Liner

> An object is an instance of a class that has its own state and behavior.

---

# 4. Attributes

Attributes are variables associated with a class or object.

## Instance Attribute

Unique to each object.

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

```python
s1 = Student("Sara", 21)
s2 = Student("Ali", 22)

print(s1.name)
print(s2.name)
```

Each object has its own `name` and `age`.

## Class Attribute

Shared by the class and normally by all instances.

```python
class Student:

    university = "University of Layyah"

    def __init__(self, name):
        self.name = name
```

```python
print(Student.university)
```

### Instance vs Class Attribute

| Instance Attribute | Class Attribute |
|---|---|
| Belongs to an object | Belongs to the class |
| Usually defined using `self` | Defined directly inside class |
| Can be different for each object | Usually shared |

---

# 5. Methods

A **method** is a function defined inside a class.

## Instance Method

Uses `self`.

```python
class Student:

    def study(self):
        print("Student is studying")
```

## Class Method

Uses `cls`.

```python
class Student:

    university = "UOL"

    @classmethod
    def show_university(cls):
        print(cls.university)
```

## Static Method

Uses neither `self` nor `cls`.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b
```

---

# 6. Constructor `__init__`

### Definition

`__init__()` is automatically called when an object is created and is used to initialize the object's state.

```python
class Book:

    def __init__(self, title, pages):
        self.title = title
        self.pages = pages


book = Book("Python", 500)
```

When this runs:

```python
book = Book("Python", 500)
```

Python creates the object and calls `__init__()` to initialize it.

### Important

The constructor is commonly called `__init__`, not `__Init__`.

Python is case-sensitive.

---

# 7. `self`

### Definition

`self` refers to the **current object / current instance**.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)
```

```python
student = Student("Sara")
student.display()
```

Conceptually:

```python
Student.display(student)
```

So `self` gives the method access to the current object's attributes and methods.

### Interview One-Liner

> `self` is a reference to the current instance of a class.

---

# 8. Object Lifecycle

A simplified object lifecycle:

```text
Class Definition
       ↓
Object Creation
       ↓
Memory/Object Initialization
       ↓
__init__()
       ↓
Object Used
       ↓
Object Becomes Unreachable
       ↓
Garbage Collection / Destruction
```

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name


student = Student("Sara")
```

When the object is created, its state is initialized.

---

# 9. Encapsulation

### Interview Definition

> **Encapsulation is the process of bundling data and methods into a single class while controlling access to the internal data.**

### Purpose

- Protect data
- Prevent accidental modification
- Add validation
- Control how data is accessed
- Hide internal implementation details

## Public

```python
class Student:

    def __init__(self):
        self.name = "Sara"
```

```python
student = Student()
print(student.name)
```

Public members are directly accessible.

## Protected

```python
self._marks = 90
```

A single underscore means:

> This member is intended for internal/subclass use.

Python does not strictly enforce protected access.

## Private

```python
self.__password = "secret"
```

Python performs **name mangling**:

```text
__password
      ↓
_Student__password
```

It discourages direct access but is not true security.

## Encapsulation Example

```python
class BankAccount:

    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount

    def get_balance(self):
        return self.__balance


account = BankAccount(5000)

account.deposit(1000)
account.withdraw(500)

print(account.get_balance())
```

The balance is controlled through methods instead of being directly modified.

## `@property`

Python provides a clean way to implement controlled attribute access.

```python
class Student:

    def __init__(self):
        self._marks = 0

    @property
    def marks(self):
        return self._marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self._marks = value
        else:
            raise ValueError("Marks must be between 0 and 100")


student = Student()
student.marks = 90

print(student.marks)
```

### Interview One-Liner

> Encapsulation protects and controls access to an object's internal state.

---

# 10. Inheritance

### Interview Definition

> **Inheritance allows a child class to acquire and extend the properties and methods of a parent class.**

### Terminology

```text
Parent Class = Base Class = Superclass

Child Class = Derived Class = Subclass
```

## Basic Example

```python
class Animal:

    def eat(self):
        print("Eating")


class Dog(Animal):

    def bark(self):
        print("Woof")


dog = Dog()

dog.eat()
dog.bark()
```

`Dog` inherits `eat()` from `Animal`.

## Types of Inheritance

### 1. Single Inheritance

```text
Animal
   ↓
Dog
```

```python
class Animal:
    pass

class Dog(Animal):
    pass
```

### 2. Multilevel Inheritance

```text
Animal
   ↓
Mammal
   ↓
Dog
```

### 3. Hierarchical Inheritance

```text
        Animal
       /      \
     Dog      Cat
```

### 4. Multiple Inheritance

```text
Teacher     Researcher
     \       /
      Professor
```

```python
class Teacher:

    def teach(self):
        print("Teaching")


class Researcher:

    def research(self):
        print("Researching")


class Professor(Teacher, Researcher):
    pass
```

## Method Overriding

A child class provides its own implementation of a parent method.

```python
class Animal:

    def sound(self):
        print("Animal sound")


class Dog(Animal):

    def sound(self):
        print("Woof")


dog = Dog()
dog.sound()
```

Output:

```text
Woof
```

### Advantages

- Code reuse
- Less duplication
- Extensibility
- Hierarchical organization

### Disadvantages

- Can create tight coupling
- Deep hierarchies become difficult to understand
- Multiple inheritance can make method resolution complex

### Interview One-Liner

> Inheritance allows a child class to reuse and specialize behavior from a parent class.

---

# 11. Polymorphism

### Interview Definition

> **Polymorphism means "many forms": different objects can respond to the same method call in different ways.**

### Key Idea

> **One interface, multiple implementations.**

## Example

```python
class Dog:

    def sound(self):
        print("Woof")


class Cat:

    def sound(self):
        print("Meow")


class Cow:

    def sound(self):
        print("Moo")


animals = [Dog(), Cat(), Cow()]

for animal in animals:
    animal.sound()
```

Output:

```text
Woof
Meow
Moo
```

The same:

```python
animal.sound()
```

produces different behavior depending on the object.

## Runtime Polymorphism

Method overriding is a common form of runtime polymorphism in Python.

## Built-in Polymorphism

```python
print(len("Python"))
print(len([1, 2, 3]))
print(len({"name": "Sara"}))
```

The same `len()` function works with different types.

### Interview One-Liner

> Polymorphism allows different objects to provide different implementations of the same interface.

---

# 12. Abstraction

### Interview Definition

> **Abstraction hides implementation details and exposes only the essential functionality or interface.**

### Real-World Example

When using:

```python
model.fit(X, y)
```

you do not need to manually implement:

- Gradient calculations
- Backpropagation
- Optimization
- Low-level numerical operations

The complex implementation is hidden behind a simple interface.

## Abstract Base Classes

Python provides the `abc` module.

```python
from abc import ABC, abstractmethod
```

## Example

```python
from abc import ABC, abstractmethod


class AIModel(ABC):

    @abstractmethod
    def predict(self):
        pass


class Chatbot(AIModel):

    def predict(self):
        return "Generating response"


class ImageClassifier(AIModel):

    def predict(self):
        return "Classifying image"


bot = Chatbot()
classifier = ImageClassifier()

print(bot.predict())
print(classifier.predict())
```

An abstract class cannot be instantiated if it has unimplemented abstract methods:

```python
model = AIModel()  # TypeError
```

### Abstract Method

```python
@abstractmethod
def predict(self):
    pass
```

Child classes are required to implement it.

### Interview One-Liner

> Abstraction hides implementation complexity and defines what a class should do rather than how it does it.

---

# 13. Class Method

### Interview Definition

> **A class method is a method that operates on the class rather than a particular instance. It receives `cls` as its first parameter.**

Syntax:

```python
@classmethod
def method(cls):
    pass
```

## Example

```python
class Student:

    university = "University of Layyah"

    @classmethod
    def show_university(cls):
        print(cls.university)


Student.show_university()
```

## Common Use: Alternative Constructor

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split(",")
        return cls(name, int(age))


student = Student.from_string("Sara,21")

print(student.name)
print(student.age)
```

### Interview One-Liner

> A class method operates on class-level state and receives `cls` as its first parameter.

---

# 14. Static Method

### Interview Definition

> **A static method is a method placed inside a class that does not depend on instance state (`self`) or class state (`cls`).**

Syntax:

```python
@staticmethod
def method():
    pass
```

## Example

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

## Validation Example

```python
class Student:

    @staticmethod
    def is_valid_age(age):
        return age >= 18


print(Student.is_valid_age(21))
```

### When to use it?

Use a static method for a utility/helper operation that is logically related to the class but does not need object or class data.

---

# 15. `super()`

### Definition

`super()` is used to access the next implementation in the class hierarchy, commonly the parent implementation.

## Constructor Example

```python
class Animal:

    def __init__(self, name):
        self.name = name


class Dog(Animal):

    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed


dog = Dog("Buddy", "Labrador")

print(dog.name)
print(dog.breed)
```

## Method Example

```python
class Animal:

    def sound(self):
        print("Animal sound")


class Dog(Animal):

    def sound(self):
        super().sound()
        print("Woof")
```

### Why use `super()`?

- Reuse parent behavior
- Avoid duplicate code
- Works correctly with inheritance hierarchies and MRO
- Important in multiple inheritance

### Interview One-Liner

> `super()` provides access to the next class implementation according to the MRO.

---

# 16. Magic / Dunder Methods

### Interview Definition

> **Magic methods are special methods whose names start and end with double underscores. They customize how objects interact with Python's built-in syntax and operations.**

Examples:

```text
__init__
__str__
__repr__
__len__
__add__
__eq__
__lt__
__call__
__getitem__
```

## `__str__()`

Controls user-friendly output.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student: {self.name}"


student = Student("Sara")

print(student)
```

## `__repr__()`

Provides a developer-oriented representation.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Student('{self.name}')"
```

## `__len__()`

```python
class Playlist:

    def __init__(self):
        self.songs = ["A", "B", "C"]

    def __len__(self):
        return len(self.songs)


playlist = Playlist()

print(len(playlist))
```

## `__add__()`

```python
class Money:

    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Money(self.amount + other.amount)

    def __str__(self):
        return str(self.amount)


m1 = Money(100)
m2 = Money(50)

print(m1 + m2)
```

## `__eq__()`

```python
class Student:

    def __init__(self, age):
        self.age = age

    def __eq__(self, other):
        return self.age == other.age


s1 = Student(21)
s2 = Student(21)

print(s1 == s2)
```

## `__call__()`

Makes an object callable like a function.

```python
class Greeter:

    def __call__(self, name):
        print(f"Hello {name}")


greet = Greeter()

greet("Sara")
```

### Interview Tip

Know these especially well:

```text
__init__
__str__
__repr__
__len__
__eq__
__add__
__call__
__getitem__
```

---

# 17. Composition

### Interview Definition

> **Composition is an OOP design technique where one class contains an object of another class and uses it to provide functionality.**

It represents a:

> **HAS-A relationship**

## Example

A car **has an engine**.

```python
class Engine:

    def start(self):
        print("Engine Started")


class Car:

    def __init__(self):
        self.engine = Engine()

    def drive(self):
        self.engine.start()
        print("Car is moving")


car = Car()
car.drive()
```

The `Car` does not inherit from `Engine`.

Instead:

```text
Car
 ↓
has an
 ↓
Engine
```

## AI Example

```python
class Logger:

    def log(self, message):
        print(message)


class AIModel:

    def __init__(self):
        self.logger = Logger()

    def train(self):
        self.logger.log("Training started")


model = AIModel()
model.train()
```

`AIModel` **has a** `Logger`.

---

# 18. Composition vs Inheritance

This is a common interview question.

| Inheritance | Composition |
|---|---|
| **IS-A** relationship | **HAS-A** relationship |
| Child extends parent | Object contains another object |
| Creates hierarchy | Combines independent components |
| Usually tighter coupling | Usually looser coupling |
| Good for specialization | Good for flexible collaboration |

## Inheritance

```text
Animal
  ↓
Dog
```

A dog **is an** animal.

```python
class Animal:
    pass

class Dog(Animal):
    pass
```

## Composition

```text
Car
 ↓
Engine
```

A car **has an** engine.

```python
class Car:

    def __init__(self):
        self.engine = Engine()
```

### When to prefer composition?

Prefer composition when:

- You have a clear **has-a** relationship.
- Components should be replaceable.
- You want loose coupling.
- You want to avoid deep inheritance hierarchies.

### Interview One-Liner

> Inheritance models "is-a", while composition models "has-a"; composition is often preferred when flexibility and loose coupling are more important than hierarchical reuse.

---

# 19. SOLID Principles

SOLID is a set of five object-oriented design principles for creating maintainable and extensible software.

```text
S → Single Responsibility Principle
O → Open/Closed Principle
L → Liskov Substitution Principle
I → Interface Segregation Principle
D → Dependency Inversion Principle
```

---

## S — Single Responsibility Principle

### Definition

> **A class should have only one responsibility and one reason to change.**

### Bad

```python
class Student:

    def calculate_grade(self):
        pass

    def save_to_database(self):
        pass

    def send_email(self):
        pass
```

Three responsibilities.

### Good

```python
class Student:

    def calculate_grade(self):
        pass


class StudentRepository:

    def save(self):
        pass


class EmailService:

    def send(self):
        pass
```

### Interview One-Liner

> One class should have one responsibility and one reason to change.

---

## O — Open/Closed Principle

### Definition

> **Software entities should be open for extension but closed for modification.**

You should be able to add new behavior without changing stable existing code.

### Bad

```python
class Payment:

    def pay(self, method):

        if method == "card":
            print("Card")

        elif method == "paypal":
            print("PayPal")
```

Every new payment method requires modifying the class.

### Better

```python
class Payment:

    def pay(self):
        pass


class CreditCard(Payment):

    def pay(self):
        print("Card")


class PayPal(Payment):

    def pay(self):
        print("PayPal")


class Crypto(Payment):

    def pay(self):
        print("Crypto")
```

### Interview One-Liner

> Add new behavior by extension rather than modifying existing stable code.

---

## L — Liskov Substitution Principle

### Definition

> **Subclasses should be usable wherever their parent class is expected without breaking program correctness.**

### Problem

```python
class Bird:

    def fly(self):
        print("Flying")


class Penguin(Bird):

    def fly(self):
        raise Exception("Penguins cannot fly")
```

A `Penguin` cannot safely substitute `Bird` when the code expects every `Bird` to fly.

### Better

```python
class Bird:

    def move(self):
        pass


class FlyingBird(Bird):

    def fly(self):
        print("Flying")


class Penguin(Bird):

    def move(self):
        print("Walking")
```

### Interview One-Liner

> A subclass should honor the behavioral contract of its parent.

---

## I — Interface Segregation Principle

### Definition

> **Clients should not be forced to depend on methods they do not need.**

### Bad

```python
class Machine:

    def print(self):
        pass

    def scan(self):
        pass

    def fax(self):
        pass
```

A basic printer shouldn't be forced to implement scanning and faxing.

### Better

```python
class Printer:

    def print(self):
        pass


class Scanner:

    def scan(self):
        pass
```

### Interview One-Liner

> Prefer small, focused interfaces over large interfaces containing unrelated methods.

In Python, interfaces are often represented using **abstract base classes or protocols**.

---

## D — Dependency Inversion Principle

### Definition

> **High-level modules should depend on abstractions, not concrete implementations.**

### Bad

```python
class MySQLDatabase:

    def save(self):
        print("Saving to MySQL")


class AIModel:

    def __init__(self):
        self.database = MySQLDatabase()
```

`AIModel` is tightly coupled to MySQL.

### Better

```python
from abc import ABC, abstractmethod


class Database(ABC):

    @abstractmethod
    def save(self):
        pass


class MySQLDatabase(Database):

    def save(self):
        print("Saving to MySQL")


class MongoDatabase(Database):

    def save(self):
        print("Saving to MongoDB")


class AIModel:

    def __init__(self, database):
        self.database = database

    def train(self):
        self.database.save()


model = AIModel(MySQLDatabase())
model.train()

model = AIModel(MongoDatabase())
model.train()
```

The dependency is injected from outside.

### Interview One-Liner

> Depend on abstractions rather than concrete implementations to reduce coupling and improve flexibility and testability.

---

# SOLID Quick Table

| Principle | Meaning | Main Goal |
|---|---|---|
| **S** | One class = one responsibility | Maintainability |
| **O** | Extend without modifying | Extensibility |
| **L** | Child can replace parent safely | Correct inheritance |
| **I** | Small focused interfaces | Avoid unnecessary dependencies |
| **D** | Depend on abstractions | Loose coupling |

### Memory Trick

```text
S → Single Job
O → Open to Extension
L → Child behaves like Parent
I → Small Interfaces
D → Depend on Abstractions
```

---

# 20. Interview Cheat Sheet

## OOP Fundamentals

| Topic | Interview Answer |
|---|---|
| **OOP** | Programming paradigm based on objects containing data and behavior |
| **Class** | Blueprint for creating objects |
| **Object** | Instance of a class |
| **Attribute** | Data associated with a class/object |
| **Method** | Function defined inside a class |
| **Constructor** | `__init__()` initializes object state |
| **`self`** | Reference to the current instance |

## Four Pillars

| Principle | Interview Answer |
|---|---|
| **Encapsulation** | Control access to internal object state |
| **Inheritance** | Reuse and extend parent behavior |
| **Polymorphism** | Same interface, different implementations |
| **Abstraction** | Hide implementation details and expose essential behavior |

## Advanced OOP

| Topic | Interview Answer |
|---|---|
| **Class Method** | Uses `cls` and operates on class-level state |
| **Static Method** | Utility method that needs neither `self` nor `cls` |
| **`super()`** | Accesses the next implementation in the MRO |
| **Magic Method** | Special `__method__` used by Python's object protocol |
| **Composition** | HAS-A relationship using contained objects |
| **Inheritance** | IS-A relationship using parent/child classes |
| **MRO** | Order Python follows to resolve methods |
| **ABC** | Defines an abstract contract for subclasses |

---

# 21. Practice Checklist

Before considering Python OOP interview preparation complete, you should be able to write these without looking at notes:

### Fundamentals

- [ ] Create a class
- [ ] Create multiple objects
- [ ] Define instance attributes
- [ ] Define class attributes
- [ ] Create instance methods
- [ ] Explain `self`
- [ ] Use `__init__()`

### Encapsulation

- [ ] Public attributes
- [ ] Protected convention `_name`
- [ ] Private/name mangling `__name`
- [ ] Getters/setters
- [ ] `@property`

### Inheritance

- [ ] Single inheritance
- [ ] Multilevel inheritance
- [ ] Hierarchical inheritance
- [ ] Multiple inheritance
- [ ] Method overriding
- [ ] `super()`
- [ ] Explain MRO

### Polymorphism

- [ ] Method overriding
- [ ] Same interface with different implementations
- [ ] Duck typing
- [ ] Built-in polymorphism

### Abstraction

- [ ] `ABC`
- [ ] `@abstractmethod`
- [ ] Create abstract base classes
- [ ] Implement subclasses

### Class & Static Methods

- [ ] `@classmethod`
- [ ] `cls`
- [ ] Alternative constructors
- [ ] `@staticmethod`
- [ ] Know when to use each method type

### Magic Methods

- [ ] `__init__`
- [ ] `__str__`
- [ ] `__repr__`
- [ ] `__len__`
- [ ] `__eq__`
- [ ] `__add__`
- [ ] `__call__`
- [ ] `__getitem__`

### Design

- [ ] Composition
- [ ] Composition vs inheritance
- [ ] IS-A vs HAS-A
- [ ] SOLID principles
- [ ] Dependency injection
- [ ] Loose coupling

---

# Final OOP Mental Model

```text
                         OOP
                          │
          ┌───────────────┴────────────────┐
          │                                │
     FUNDAMENTALS                     CORE PRINCIPLES
          │                                │
   Class / Object                    Encapsulation
   Attributes                        Inheritance
   Methods                           Polymorphism
   __init__                          Abstraction
   self
          │
          └───────────────┬────────────────┘
                          │
                    ADVANCED OOP
                          │
        ┌─────────────────┼──────────────────┐
        │                 │                  │
   Class Method      Static Method       Magic Methods
   super()           MRO                 ABC
        │
        └─────────────────┬──────────────────┘
                          │
                    DESIGN PRINCIPLES
                          │
                       SOLID
                          │
                ┌─────────┼─────────┐
                │         │         │
             SRP/OCP    LSP/ISP     DIP
                          │
                          ↓
                 Composition & Design
                          │
                          ↓
              Production-Ready OOP
```

---

# Quick Interview Formula

For almost every OOP question, answer in this order:

```text
1. Definition
2. Why we use it
3. Small code example
4. Real-world example
5. Difference from related concept
```

For example:

**"What is polymorphism?"**

> Polymorphism means one interface with multiple implementations. It allows different objects to respond differently to the same method call. In Python, method overriding and duck typing are common examples. For instance, different AI models can all implement `predict()` differently.

---

# Final Goal

For an **AI-Powered Full Stack Engineer**, you should be comfortable using OOP when building:

- Flask/FastAPI backends
- AI/ML model services
- RAG pipelines
- Database repositories
- Authentication services
- API clients
- LLM integrations
- File/storage services
- Testing and mockable components
- Production application architecture

The goal is not just to memorize OOP definitions. You should be able to **design classes, choose composition vs inheritance, apply SOLID, and explain your design decisions in an interview.**
