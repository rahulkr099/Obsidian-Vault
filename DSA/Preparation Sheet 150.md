### Write a program to check whether a number is even or not.

**Modulo:** num % 2 == 0
**Bitwise AND:** num & 1 == 0
**Division & Multiplication:** ( num // 2) *  2 == num
## 🚀 Practice ideas (to improve)

1. Take **10 numbers from user** and classify
2. Count how many are **odd** and **even**
3. Print only even numbers from a list
4. Print all even numbers between 1 and N
5. Write the same logic using **list comprehension**
```python
evens = [n for n in range(1, 21) if n % 2 == 0]
print(evens)
```

