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

## 🔥 Next-Level Ideas (Interview-ready)

20. Find **nearest prime** to a given number
    
21. Check if a number is a **product of two primes**
    
22. Find longest sequence of consecutive primes in a range
    
23. Use sieve to answer **multiple prime queries fast**