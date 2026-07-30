# Class Real Life Example

Real-life analogies make OOP much easier to understand.

Here are many simple and intuitive examples.

---

# 1. Car Example

```
Class  → Car blueprint/design
Object → Actual Tesla, BMW, Audi cars
```

One design can create many cars.

---

# 2. House Example

```
Class  → House map/design
Object → Actual built houses
```

Different houses can be built from same design.

---

# 3. Student Example

```
Class  → Student form/template
Object → Rahul, Aman, Priya
```

Each student has different data:

- name
- age
- roll number

but same structure.

---

# 4. Mobile Phone Example

```
Class  → Phone model design
Object → Individual phones
```

Example:

```
Class  → iPhone 15 Design
Objects → Your iPhone, my iPhone
```

---

# 5. Cookie Cutter Example

Very famous OOP analogy.

```
Class  → Cookie cutter
Object → Actual cookies
```

One cutter creates many cookies.

---

# 6. Building Blueprint

```
Class  → Building blueprint
Object → Actual apartments/buildings
```

Blueprint defines:

- rooms
- doors
- windows

---

# 7. Human Example

```
Class  → Human
Objects → Rahul, Aman, Neha
```

Common features:

- name
- age
- speak()
- walk()

---

# 8. Animal Example

```
Class  → Dog
Objects → Tommy, Rocky, Bruno
```

Each object has:

```
same behaviors:
- bark()
- eat()

different data:
- name
- color
```

---

# 9. Bank Account Example

```
Class  → BankAccount
Objects → Your account, my account
```

Each account has:

- account number
- balance

Methods:

- deposit()
- withdraw()

---

# 10. Restaurant Menu Example

```
Class  → Pizza recipe
Object → Actual pizzas
```

Many pizzas can be made from one recipe.

---

# 11. Employee Example

```
Class  → Employee structure
Objects → Employees in company
```

Common structure:

- name
- salary
- department

---

# 12. YouTube Channel Example

```
Class  → Video template/system
Objects → Individual uploaded videos
```

Each video has:

- title
- views
- likes

---

# 13. Game Character Example

```
Class  → Character type
Objects → Different players
```

Methods:

- attack()
- run()
- jump()

Attributes:

- health
- power
- speed

---

# 14. ATM Machine Example

```
Class  → ATM software design
Objects → Actual ATM machines
```

Each ATM works similarly.

---

# 15. Laptop Example

```
Class  → Laptop model
Objects → Individual laptops
```

---

# 16. Book Example

```
Class  → Book category/template
Objects → Individual books
```

Attributes:

- title
- author
- price

---

# 17. University Example

```
Class  → Course structure
Objects → Actual students enrolled
```

---

# 18. Bicycle Example

```
Class  → Bicycle design
Objects → Actual bicycles
```

Methods:

- brake()
- pedal()

---

# 19. Movie Example

```
Class  → Movie template
Objects → Different movies
```

Properties:

- name
- duration
- rating

---

# 20. WhatsApp User Example

```
Class  → WhatsApp user structure
Objects → Actual user accounts
```

Methods:

- send_message()
- call()

Attributes:

- name
- phone number

---

# Best Way to Think About Classes and Objects

---

# Class

A class is:

```
Plan
Design
Template
Blueprint
Structure
```

It describes WHAT something should look like.

---

# Object

An object is:

```
Real usable thing
Created from class
```

---

# Super Important Visualization

```
          CLASS
      (Blueprint)

             ↓

     Object 1
     Object 2
     Object 3
```

---

# One More Powerful Example

## Instagram

```
Class  → Instagram User structure
Object → Actual accounts
```

Each account has:

Attributes:

- username
- followers
- bio

Methods:

- post()
- follow()
- message()

---

# OOP in Real Life

Almost everything around you can be modeled as:

```
Class + Object
```

Examples:

|Real Thing|Class|Object|
|---|---|---|
|Car|Car|Tesla|
|Human|Human|Rahul|
|Dog|Dog|Tommy|
|Phone|Phone|Samsung|
|Account|BankAccount|Your account|

---

# Golden Rule

```
Class = Common Structure
Object = Real Individual Instance
```

---

# Easy Trick to Identify

Ask:

```
Can many similar things be made from this?
```

If YES:

```
That is probably a class.
```

---

# 1. Creating Your First Class

```python
class Student:
    pass
```

### Explanation

- `class` keyword is used to create a class.
- `Student` is the class name.
- `pass` means “nothing inside yet”.

---

# 2. Creating an Object

```python
class Student:
    pass

s1 = Student()

print(s1)
```

### Output

```python
<__main__.Student object at 0x...>
```

Here:

- `Student()` creates an object.
- `s1` stores that object.

---

# 3. Adding Data to Class using `__init__`

The `__init__` method is called automatically when an object is created.

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Now create objects:

```python
s1 = Student("Rahul", 21)
s2 = Student("Aman", 22)

print(s1.name)
print(s1.age)

print(s2.name)
```

### Output

```python
Rahul
21
Aman
```

---

# Understanding `self`

`self` means:

> “This current object”

When you write:

```python
self.name = name
```

It means:

```python
s1.name = "Rahul"
```

for that specific object.

---

# 4. Adding Methods (Functions inside Class)

```python
class Student:

    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hello, my name is {self.name}")
```

Create object:

```python
s1 = Student("Rahul")

s1.greet()
```

### Output

```python
Hello, my name is Rahul
```

---

# 5. Real Life Example

```python
class Car:

    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

    def drive(self):
        print(f"{self.brand} car is driving")
```

Object creation:

```python
car1 = Car("Tesla", "Black")
car2 = Car("BMW", "White")

print(car1.brand)
print(car2.color)

car1.drive()
```

---

# Internal Flow

When you do:

```python
car1 = Car("Tesla", "Black")
```

Python internally does:

1. Creates empty object
2. Passes object to `self`
3. Calls `__init__`
4. Stores values inside object

---

# Important Terms

|Term|Meaning|
|---|---|
|Class|Blueprint|
|Object|Instance of class|
|Attribute|Variables inside object|
|Method|Functions inside class|
|`self`|Current object|
|`__init__`|Constructor|

---

# Multiple Objects Example

```python
class Dog:

    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name} says Woof!")
```

```python
d1 = Dog("Tommy")
d2 = Dog("Rocky")

d1.bark()
d2.bark()
```

### Output

```python
Tommy says Woof!
Rocky says Woof!
```

Notice:

- Same class
- Different objects
- Different data

---

# Memory Visualization

```
Class: Student

Object 1:
name = Rahul
age = 21

Object 2:
name = Aman
age = 22
```

---

# Beginner Mistakes

## Forgetting `self`

❌ Wrong:

```python
def greet():
```

✅ Correct:

```python
def greet(self):
```

---

## Forgetting object creation

❌ Wrong:

```python
Student.greet()
```

✅ Correct:

```python
s1 = Student("Rahul")
s1.greet()
```

---

---

# Most Important Concept

A class groups:

- data (variables)
- behavior (functions)

together into one structure.

That is the heart of Object Oriented Programming (OOP).

---

# Class and Object Namespace

In Python, both **classes** and **objects** have their own **namespace**.

A **namespace** is simply:

> A place where names (variables and functions) are stored.

Think of it like a dictionary internally.

---

# Simple Meaning of Namespace

Python stores variables like this:

```python
{
   "name": "Rahul",
   "age": 21
}
```

This storage area is called a **namespace**.

---

# Types of Namespace in Classes and Objects

There are mainly two important namespaces here:

|Namespace|Belongs To|
|---|---|
|Class Namespace|Class itself|
|Object Namespace|Individual object|

---

# 1. Class Namespace

Variables written directly inside class belong to the **class namespace**.

Example:

```python
class Student:

    school = "ABC School"
```

Here:

```python
school
```

belongs to the class namespace.

---

## Accessing Class Namespace

```python
print(Student.school)
```

Output:

```python
ABC School
```

---

# 2. Object Namespace

Variables created using `self` belong to the object namespace.

Example:

```python
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name
```

Now:

```python
s1 = Student("Rahul")
```

Object namespace of `s1` contains:

```python
{
   "name": "Rahul"
}
```

---

# Visualization

```
Class Namespace
----------------
school = "ABC School"

Object Namespace (s1)
---------------------
name = "Rahul"

Object Namespace (s2)
---------------------
name = "Aman"
```

---

# Very Important Rule

Python first searches inside:

```
Object Namespace
      ↓
Class Namespace
```

This is called:

## Namespace Lookup

---

# Example of Lookup

```python
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name
```

```python
s1 = Student("Rahul")

print(s1.name)
print(s1.school)
```

---

## How Python Searches

### `s1.name`

Python checks:

```
s1 object namespace
```

Finds:

```python
name = "Rahul"
```

Done.

---

### `s1.school`

Python checks:

```
1. s1 object namespace ❌
2. Student class namespace ✅
```

Finds:

```python
school = "ABC School"
```

---

# Object Can Override Class Variable

```python
class Student:

    school = "ABC School"
```

```python
s1 = Student()

s1.school = "XYZ School"
```

Now:

```python
print(s1.school)
print(Student.school)
```

Output:

```python
XYZ School
ABC School
```

---

# Why?

Because:

```python
s1.school = "XYZ School"
```

creates a new variable inside object namespace.

Now object namespace has:

```python
{
   "school": "XYZ School"
}
```

Python finds it first.

---

# Accessing Namespace Directly

Every object has:

```python
__dict__
```

which shows its namespace.

---

# Object Namespace

```python
class Student:

    def __init__(self, name):
        self.name = name
```

```python
s1 = Student("Rahul")

print(s1.__dict__)
```

Output:

```python
{'name': 'Rahul'}
```

---

# Class Namespace

```python
class Student:

    school = "ABC School"
```

```python
print(Student.__dict__)
```

Output (simplified):

```python
{
   'school': 'ABC School'
}
```

---

# Full Example

```python
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name
```

```python
s1 = Student("Rahul")
s2 = Student("Aman")
```

---

## Namespaces

### Class Namespace

```python
{
   'school': 'ABC School'
}
```

### Object Namespace of s1

```python
{
   'name': 'Rahul'
}
```

### Object Namespace of s2

```python
{
   'name': 'Aman'
}
```

---

# Important Interview Concept

## Class Variable

Shared by all objects.

```python
class Student:
    school = "ABC"
```

---

## Instance Variable

Unique for every object.

```python
self.name = name
```

---

# Memory View

```
                Student Class
         -------------------------
         school = "ABC School"
         greet()

             ↑         ↑
             |         |

         s1 Object   s2 Object
        ------------ ------------
        name=Rahul   name=Aman
```

---

# Key Understanding

|Thing|Stored In|
|---|---|
|Class variables|Class namespace|
|Instance variables|Object namespace|
|Methods|Class namespace|

---

# One More Important Thing

Methods are stored in class namespace.

```python
class Student:

    def greet(self):
        print("Hello")
```

`greet` belongs to the class namespace.

Objects access it through lookup.

---

# Actual Lookup Chain

When you do:

```python
s1.greet()
```

Python searches:

```
1. Object namespace
2. Class namespace
3. Parent classes
```

This is called:

# MRO (Method Resolution Order)

You’ll study this deeply in inheritance.

---

# Super Important Summary

## Class Namespace

Shared data and methods.

```python
class Student:
    school = "ABC"
```

---

## Object Namespace

Personal object data.

```python
self.name = name
```

---

## Lookup Order

```
Object → Class → Parent Class
```

---

# Best Way to Remember

```
Class = Common Things
Object = Personal Things
```

Example:

```
School name → common → class variable

Student name → personal → instance variable
```

# Attribute Shadowing

# Attribute Shadowing in Python

Attribute shadowing happens when:

> An object variable hides a class variable with the same name.

Python always searches in this order:

```
Object Namespace → Class Namespace
```

So if the object already has an attribute with the same name, Python stops there.

---

# Basic Example

```python
class Student:

    school = "ABC School"
```

Create object:

```python
s1 = Student()

print(s1.school)
```

Output:

```python
ABC School
```

Why?

Because Python searches:

```
1. s1 object namespace ❌
2. Student class namespace ✅
```

---

# Now Shadow the Attribute

```python
s1.school = "XYZ School"
```

Now:

```python
print(s1.school)
print(Student.school)
```

Output:

```python
XYZ School
ABC School
```

---

# What Happened?

This line:

```python
s1.school = "XYZ School"
```

does NOT change the class variable.

Instead, Python creates a NEW variable inside the object namespace.