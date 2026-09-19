# DAY 1 - LLD: OOP Fundamentals for System Design
# How should we think about LLD problems 
Clarify the requirements -> Define what Objects you need -> What responsiblity each object will have -> What is the relationship between them -> What Classes/Interfaces needed -> ACTCUAL CODE WRITING 

# Object-Oriented Programming is based around objects.
Objects has two things 
* Data/Atributes/Propeties 
* Behaviour/verb/action 
```python
class Car:
    # THESE ARE DATA
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    # THESE ARE BEHVIOUR
    def accelerate(self):
        print("Car accelerating")

    def brake(self):
        print("Car braking")
```
# Class vs Object
Class = blueprint  
Object = actual thing

```python 
# CLASS 
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name} says Woof!")

# OBJECTS 
dog1 = Dog("Bruno")
dog2 = Dog("Max")
```

# Encapsulation (public vs private)
Keep an object's internal state and implementation details controlled behind a public interface.

```python 
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self._balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        if amount > self._balance:
            raise ValueError("Insufficient balance")

        self._balance -= amount

    def get_balance(self):
        return self._balance
```
The caller doesn't need to know how balance is stored.
```python 
account.deposit(1000)
account.withdraw(300)
```

# Abstraction
Expose only what the user needs to know. BUT My defination is it implemets methods which future classes will use or methods whihc future class will use but no need to implement. It itself does not have any implementation.

```python
from abc import ABC, abstractmethod

# You cannot create an object of this class directly
class Animal(ABC):
    
    # 1. Abstract method: Has NO implementation. 
    # Every specific animal must decide how it makes a sound.
    @abstractmethod
    def make_sound(self):
        pass

    # 2. Concrete method: Has FULL implementation.
    # All animals sleep the same way, so we write the code here once.
    def sleep(self):
        print("Zzz... this animal is sleeping.")

# Dog inherits from Animal
class Dog(Animal):
    # We MUST implement the abstract method here
    def make_sound(self):
        print("Woof! Woof!")

# Cat inherits from Animal
class Cat(Animal):
    # We MUST implement the abstract method here
    def make_sound(self):
        print("Meow!")

if __name__ == "__main__":
    # my_animal = Animal() # ERROR! Cannot instantiate an abstract class
    
    my_dog = Dog()
    my_cat = Cat()

    # Using the implemented method from the abstract class
    my_dog.sleep() # Outputs: Zzz... this animal is sleeping.
    my_cat.sleep() # Outputs: Zzz... this animal is sleeping.

    # Using the methods implemented by the future classes
    my_dog.make_sound() # Outputs: Woof! Woof!
    my_cat.make_sound() # Outputs: Meow!

```

# Inheritance
Inheritance means one class derives behavior/structure from another.

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")
```

# Polymorphism
The same interface can represent different implementations. method overloading and method overriding is polymorphisum.

```python 
class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
# DIFFIRENT IMPLEMENTATION 
class UPIPayment(PaymentProcessor):

    def pay(self, amount):
        print("UPI payment")


class CardPayment(PaymentProcessor):

    def pay(self, amount):
        print("Card payment")
```
# ASSOCIATION 
Two objects know about or interact with each other.
# AGGREGATION
week HAS-a relationship 
Department ----> Teacher 
# COMPOSITION 
strong HAS-a(owner) relationship
House ---> Room 

```
Doctor ───── Patient
   association


Team ◇────── Player
   aggregation


House ◆───── Room
   composition
```

# Dependency
One object temporarily relies on another object to perform some operation.

```python
class ReportService:

    def generate(self, printer):
        printer.print("Report") # Printer => another service 
```

# Coupling
Coupling measures how strongly components depend on each other.
`Generally: Prefer low coupling.`

# Cohesion
```python
# THIS IS BAD It should have been diffrent services like Email service, payment service 

# Unrealted repos more == lowerr cohesion 
class UserManager:
    create_user()
    send_email()
    process_payment()
    generate_invoice()
    resize_image()
    connect_database() 
```
```High cohesion + low coupling```

# HOMEWORK
## DAY 1 HOMEWORK — Library Management System

Now your actual assignment.

Requirements

Design a simple library system.

The system should support:

* Multiple books.
* Multiple members.
* A member can borrow a book.
* A member can return a book.
* A book can be available or borrowed.
* The system should track who borrowed a book.
* A member can borrow multiple books.  
Your task
Do NOT write the complete code yet.
First design the objects.
```
Give me:

1. Classes
2. Important attributes
3. Important methods
4. Relationships between classes
5. Responsibility of each class
```
For example, your answer should look roughly like:
```
Class: Book

Attributes:
- ...
- ...

Methods:
- ...
- ...

Responsibility:
- ...
```
Then explain relationships:
```
Library → ?
Member → ?
Book → ?
```