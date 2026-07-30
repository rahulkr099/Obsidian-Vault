In Python, `enumerate()` is used when you want **both**:

- the **index (position)** of an item
- and the **item itself**

while looping through a list (or any iterable).

---

## Syntax

```python
enumerate(iterable, start=0)
```

- `iterable` → list, tuple, string, etc.
- `start` → index starting value (default is `0`)

---

## Without `enumerate()`

```python
fruits = ["apple", "banana", "mango"]

index = 0

for fruit in fruits:
    print(index, fruit)
    index += 1
```

Output:

```python
0 apple
1 banana
2 mango
```

This works, but manually managing `index += 1` is not clean.

---

## With `enumerate()`

```python
fruits = ["apple", "banana", "mango"]

for index, fruit in enumerate(fruits):
    print(index, fruit)
```

Output:

```python
0 apple
1 banana
2 mango
```

Cleaner and more Pythonic.

---

## Why use `enumerate()`?

## 1. Cleaner code

Instead of manually increasing index:

```python
i += 1
```

Python handles it automatically.

---

## 2. Easier to read

```python
for index, item in enumerate(data):
```

Anyone reading the code instantly understands:

“we need index + value”.

---

## 3. Avoid bugs

Manual index management can cause mistakes.

Example:

```python
i = 0

for item in items:
    # forgot i += 1
```

`enumerate()` removes this problem.

---

# Zip

`zip()` in Python is used to **combine multiple iterables together** element by element.

It pairs items based on their positions.

## Real-World Use Cases

## 1. Combining related data

```python
users= ["Rahul","Aman"]
emails= ["r@gmail.com","a@gmail.com"]

for user,email in zip(users,emails):
print(user,email)
```

Very common in backend development.

---

## 2. Creating Dictionary

```python
keys= ["name","age","city"]
values= ["Rahul",21,"Sitamarhi"]

data=dict(zip(keys,values))

print(data)
```

Output:

```
{'name':'Rahul','age':21,'city':'Sitamarhi'}
```

---

## 3. Looping through 3 lists

```python
names= ["A","B","C"]
marks= [90,80,70]
grades= ["A+","B+","C+"]

forname,mark,grade in zip(names,marks,grades):
print(f"{names} scored {marks} : {grades}")
```

---

# Walrus Operator

The `:=` operator is called the **Walrus Operator** in Python.

It was introduced in **Python 3.8**.

It allows you to:

- **assign a value**
- and **use it immediately in an expression**

at the same time.

```python
value = 13

remainder = value % 5

if remainder: 
	print(f"Not divisible, remainder is {remainder}")
######
value = 13

if remainder := value % 5:
	print(f"Not divisible, remainder is {remainder}")

##########33

available_sizes = ["small", "medium", "large"]

if (requested_size := input("Enter your chai cup size: ")) in available_sizes:
	print(f"Serving {requested_size} chai")
else:
	print(f"Size is unavailable - {requested_size}")
############
	
flavors = ["masala", "ginger", "lemon", "mint"]

print("Available flavors: ", flavors)

while (flavor := input("Choose your flavor: " )) not in flavors:
	print(f"Sorry, {flavor} is not available")
	
print(f"You chose {flavor} chai")
```

## Why use Walrus Operator?

## 1. Avoid repeating calculations

Without walrus:

```
value=input()

iflen(value)>5:
print(len(value))
```

`len(value)` runs twice.

---

With walrus:

```
if (length:=len(value))>5:
print(length)
```

Cleaner and faster.

```python
:=  means
"store this value AND use it immediately"
```

`match-case` in Python is similar to:

- `switch-case` in C/C++/Java
- pattern matching systems in modern languages

```python
method = "POST"

match method:
    case "GET":
        print("Fetch data")
    case "POST":
        print("Create data")
    case "PUT":
        print("Update data")
    case "DELETE":
        print("Delete data")
```

## Dictionary in place of match case

```python
users = [
    {"id": 1, "total": 100, "coupon": "P20"},
    {"id": 2, "total": 150, "coupon": "F10"},
    {"id": 3, "total": 80, "coupon": "P50"},
]

discounts = {
    "P20": (0.2, 0),
    "F10": (0.5, 0),
    "P50": (0, 10),
}

for user in users:
    percent, fixed = discounts.get(user["coupon"], (0, 0))
    discount = user["total"] * percent + fixed

    print(
        f"{user['id']} paid {user['total']} and got "
        f"discount for next visit of rupees {discount}"
    )
```

## Dictionary of Functions

Very common in real projects.

```python
defadd():
print("Adding")

defdelete():
print("Deleting")

actions= {
"add":add,
"delete":delete,
}

actions["add"]()
```

Output:

```
Adding
```

This behaves like a switch statement.

---

## Difference Between Dictionary Mapping vs Match Case

|Feature|Dictionary Mapping|Match Case|
|---|---|---|
|Best for key-value lookup|✅|❌|
|Best for complex patterns|❌|✅|
|Easy to extend|✅|Medium|
|Supports pattern matching|❌|✅|
|Common in backend systems|✅ Very common|Sometimes|