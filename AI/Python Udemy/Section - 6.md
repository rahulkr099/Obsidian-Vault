In Python, `global` and `nonlocal` are used when you want to modify variables outside the current function scope.

They are related to **scope**.

---

# 1. `global` Keyword

`global` is used to modify a variable that exists in the **global scope** (outside all functions).

## Example Without `global`

```python
x = 10

def change():
    x = 20
    print(x)

change()
print(x)
```

### Output

```python
20
10
```

Why?

Because inside `change()`, Python creates a **new local variable** `x`.

The global `x` remains unchanged.

---

## Example With `global`

```python
x = 10

def change():
    global x
    x = 20
    print(x)

change()
print(x)
```

### Output

```python
20
20
```

Now Python understands:

> "Use the global variable `x`, not a local one."

---

# 2. `nonlocal` Keyword

`nonlocal` is used inside **nested functions**.

It modifies a variable from the **outer function**, not the global scope.

---

## Example Without `nonlocal`

```python
def outer():
    x = 10

    def inner():
        x = 20
        print("Inner:", x)

    inner()
    print("Outer:", x)

outer()
```

### Output

```python
Inner: 20
Outer: 10
```

Again, `inner()` created its own local `x`.

---

## Example With `nonlocal`

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20
        print("Inner:", x)

    inner()
    print("Outer:", x)

outer()
```

### Output

```python
Inner: 20
Outer: 20
```

Now `inner()` modifies the variable from `outer()`.

---

# Simple Difference

|Keyword|Works With|Used In|
|---|---|---|
|`global`|Global variable|Normal functions|
|`nonlocal`|Outer function variable|Nested functions|

---

# Scope Hierarchy in Python

Python follows LEGB rule:

|Scope|Meaning|
|---|---|
|L|Local|
|E|Enclosing (`nonlocal`)|
|G|Global|
|B|Built-in|

---

# Real Visualization

```python
name = "Global"

def outer():
    name = "Outer"

    def inner():
        name = "Inner"
```

Here:

- `Inner` → Local
- `Outer` → Enclosing (`nonlocal`)
- `Global` → Global

---

# Important Note

`nonlocal` cannot access global variables directly.

This is invalid:

```python
x = 10

def test():
    nonlocal x   # ERROR
```

Because `x` is not in an enclosing function.

---

# Interview-Friendly Memory Trick

- `global` → go outside all functions
- `nonlocal` → go one level outside current function

---

# One Combined Example

```python
x = 100

def outer():
    y = 50

    def inner():
        global x
        nonlocal y

        x += 1
        y += 1

        print(x, y)

    inner()

outer()

print(x)
```

### Output

```python
101 51
101
```

Here:

- `x` came from global scope
- `y` came from enclosing scope

This type of question is very common in Python interviews.

In Python:

- `args` → accepts multiple **positional arguments**
- `*kwargs` → accepts multiple **keyword arguments**

They make functions flexible.

---

# 1. `args`

`args` stands for **arguments**.

It collects extra positional values into a **tuple**.

---

## Example

```python
def add(*args):
    print(args)

add(1, 2, 3, 4)
```

### Output

```python
(1, 2, 3, 4)
```

Python packed all values into a tuple.

---

## Loop Through `args`

```python
def add(*args):
    total = 0

    for num in args:
        total += num

    print(total)

add(1, 2, 3)
```

### Output

```python
6
```

---

# Why Use `args`?

Suppose you don't know how many arguments users will pass.

Without `args`:

```python
def add(a, b):
    return a + b
```

Only 2 values allowed.

But with `*args`, unlimited values work.

---

# 2. `*kwargs`

`kwargs` stands for **keyword arguments**.

It collects named arguments into a **dictionary**.

---

## Example

```python
def person(**kwargs):
    print(kwargs)

person(name="Rahul", age=21)
```

### Output

```python
{'name': 'Rahul', 'age': 21}
```

---

## Loop Through `kwargs`

```python
def person(**kwargs):

    for key, value in kwargs.items():
        print(key, value)

person(name="Rahul", age=21)
```

### Output

```python
name Rahul
age 21
```

---

# Difference Between `args` and `kwargs`

|Feature|`*args`|`**kwargs`|
|---|---|---|
|Takes|Positional arguments|Keyword arguments|
|Stores in|Tuple|Dictionary|
|Symbol|`*`|`**`|

---

# Combined Example

```python
def demo(*args, **kwargs):
    print(args)
    print(kwargs)

demo(1, 2, 3, name="Rahul", age=21)
```

### Output

```python
(1, 2, 3)
{'name': 'Rahul', 'age': 21}
```

---

# Important Rule Order

When writing parameters:

```python
def test(normal, *args, **kwargs):
    pass
```

Correct order:

1. Normal parameters
2. `args`
3. `*kwargs`

---

# Real-Life Usage

Frameworks like:

- Django
- Flask
- FastAPI

use `args` and `kwargs` heavily for flexible APIs.

---

# Memory Trick

```python
*args   -> many values
**kwargs -> many named values
```

---

# Bonus: Unpacking

You can also use `*` and `**` to unpack data.

## Unpack List

```python
nums = [1, 2, 3]

print(*nums)
```

Output:

```python
1 2 3
```

---

## Unpack Dictionary

```python
data = {
    "name": "Rahul",
    "age": 21
}

def person(name, age):
    print(name, age)

person(**data)
```

Output:

```python
Rahul 21
```

---

# Interview Question

## Is `args` and `kwargs` name compulsory?

No.

Only `*` and `**` matter.

These are valid too:

```python
def test(*numbers, **details):
    pass
```

But people mostly use:

- `args`
- `kwargs`

because they are standard conventions.

Your code has an important concept related to **mutable default arguments** in Python.

But your function currently does nothing because `order` is never used or returned.

Let’s properly understand it.

---

# Your Code

```python
def chai_order(order=None):
    if order is None:
        order = []

chai_order()
chai_order()
```

This runs perfectly fine.

But nothing happens because:

- no `print()`
- no `return`

---

# Why Use `None` Here?

This is done to avoid a very famous Python problem.

---

# Wrong Way (Dangerous)

```python
def chai_order(order=[]):
    order.append("Tea")
    print(order)

chai_order()
chai_order()
```

### Output

```python
['Tea']
['Tea', 'Tea']
```

Why?