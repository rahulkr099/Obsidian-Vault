Generators in Python are functions that produce values one at a time using the `yield` keyword.

They work together with the `next()` function.

This is one of the most important Python concepts for backend, async systems, streaming, and memory-efficient programming.

---

# Normal Function vs Generator Function

## Normal Function

```python
def greet():
    return "Hello"

print(greet())
```

Output:

```python
Hello
```

Function ends after `return`.

---

# Generator Function

```python
def count():
    yield 1
    yield 2
    yield 3
```

This does NOT return all values immediately.

It returns a **generator object**.

```python
nums = count()

print(nums)
```

Output:

```python
<generator object count at ...>
```

---

# Using `next()`

`next()` asks generator for the next value.

```python
def count():
    yield 1
    yield 2
    yield 3

nums = count()

print(next(nums))
print(next(nums))
print(next(nums))
```

Output:

```python
1
2
3
```

---

# What Happens Internally?

Generator pauses at every `yield`.

Think like this:

```python
yield = pause and remember everything
```

When `next()` runs again:

- function resumes from where it stopped
- local variables remain saved

This is super powerful.

---

# Visualization

```python
def demo():
    print("Start")
    yield 1

    print("Middle")
    yield 2

    print("End")
    yield 3
```

Execution:

```python
d = demo()

print(next(d))
```

Output:

```python
Start
1
```

Second call:

```python
print(next(d))
```

Output:

```python
Middle
2
```

Third call:

```python
print(next(d))
```

Output:

```python
End
3
```

---

# After Completion

```python
print(next(d))
```

Output:

```python
StopIteration
```

Generator is exhausted.

---

# Important: State is Preserved

```python
def counter():
    num = 1

    while num <= 3:
        yield num
        num += 1

c = counter()

print(next(c))
print(next(c))
print(next(c))
```

Output:

```python
1
2
3
```

Notice:

- variable `num` remembers its value
- function does NOT restart

---

# Generator with Loop

```python
def squares(n):
    for i in range(n):
        yield i * i

gen = squares(5)

for value in gen:
    print(value)
```

Output:

```python
0
1
4
9
16
```

---

# Infinite Generator

Very important concept.

```python
def infinite():
    num = 1

    while True:
        yield num
        num += 1
```

Usage:

```python
gen = infinite()

print(next(gen))
print(next(gen))
print(next(gen))
```

Output:

```python
1
2
3
```

Useful in:

- live streams
- real-time systems
- event processing
- backend queues

---

# Difference Between `return` and `yield`

|return|yield|
|---|---|
|Ends function|Pauses function|
|Returns one value|Produces many values|
|State lost|State preserved|
|Function finishes|Function resumes later|

---

# `yield` vs List

## List

```python
def nums():
    return [1, 2, 3]
```

Everything created at once.

---

## Generator

```python
def nums():
    yield 1
    yield 2
    yield 3
```