### Write a program to check whether a number is even or not.

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

### 2. WAP to determine if a number is prime.


## 🧠 Prime Number – Core Idea

A number is **prime** if:

- It is greater than `1`
    
- It has **only two divisors** → `1` and itself
    

---

## 📝 PSEUDO CODE (Interview Friendly)

### Prime Check using Square Root Optimization

```
START
  INPUT number n

  IF n <= 1
     PRINT "Not Prime"
     STOP

  FOR i from 2 to √n
     IF n mod i == 0
        PRINT "Not Prime"
        STOP
     END IF
  END FOR

  PRINT "Prime"
END
```

👉 This pseudo code is **exactly what interviewers expect**

---


## ❌ Common Interview Mistakes (Avoid These)

❌ Checking till `n - 1`  
❌ Forgetting `n <= 1` case  
❌ Ignoring time complexity  
❌ Saying “prime means divisible by 2” 😅

---

# 🎯 Interview Practice Challenges (Very Important)

### 🔹 Beginner Level

1. Check if a number is prime
    
2. Print all primes from `1 to N`
    
3. Count prime numbers in a range
    
4. Prime check using `while` loop
    

---

### 🔹 Intermediate Level

5. Skip even numbers in prime check
    
6. Find prime numbers in a list
    
7. Find **largest prime factor**
    
8. Check if number is **prime + palindrome**
    

---

### 🔹 Advanced / WOW Level

9. Prime check using **recursion**
    
10. Generate primes using **Sieve of Eratosthenes**
    
11. Count primes up to `N` efficiently
    
12. Precompute primes for fast queries
    
13. Prime checking for very large numbers
    
14. Explain time complexity comparison
    

---

## 🧠 Interview Tip (Gold Answer)

If interviewer asks:

> “Why do you check till √n?”

Say:

> “Because if a number has a factor greater than √n, the other factor must be smaller than √n.”

That answer = ⭐ extra confidence points

---

### 3. WAP to check if a given year is a leap year.
## Practice Challenges (Level Up)

Try solving:

1. Print all leap years from 1900 to 2100
    
2. Count leap years in last 100 years
    
3. Check leap year using **bitwise operator**
    
4. Convert leap year logic into **pseudo code**
    
5. Handle invalid inputs (negative years)

# 4. Calculating Armstrong Numbers
## 🧠 Basic Logic (Step-by-Step)

1. Store the original number
    
2. Count number of digits
    
3. Extract each digit
    
4. Raise digit to power of digit count
    
5. Add them
    
6. Compare with original number
## 🧠 Important Edge Cases (Interview Trap)

- Single-digit numbers → **Always Armstrong** (`0–9`)
    
- Very large numbers
    
- Negative numbers (usually ❌)
    
- Input as string vs integer
    

---

## 🎯 Interview Practice Challenges (Must Try)

### 🔹 Beginner Level

1. Check if a number is Armstrong
    
2. Print all Armstrong numbers from `1–1000`
    
3. Count Armstrong numbers in a range
    
4. Check Armstrong using `while` loop only
    

---

### 🔹 Intermediate Level

5. Find Armstrong numbers in a **list**
    
6. Write logic **without converting to string**
    
7. Compare Armstrong and Prime numbers
    
8. Find Armstrong numbers with exactly `k` digits
    

---

### 🔹 Advanced / WOW Questions

9. Time complexity analysis
    
10. Armstrong number using **recursion**
    
11. Precompute powers for optimization
    
12. Armstrong numbers up to `10^6` efficiently
    
13. Create a **generator** for Armstrong numbers
    
14. Check Armstrong in **any base (base-n)**


# 4. Generating the Fibonacci Series
```
START
  INPUT n
  SET a = 0, b = 1

  IF n <= 0
     STOP

  PRINT a

  FOR i from 2 to n
     PRINT b
     SET next = a + b
     SET a = b
     SET b = next
  END FOR
END


```

## ❌ Common Interview Mistakes

❌ Mixing series and nth term  
❌ Infinite loop  
❌ Not handling `n = 0`  
❌ Using recursion without optimization

---

# 🎯 Interview Practice Challenges (Must Do)

### 🔹 Beginner Level

1. Print Fibonacci series up to `N`
    
2. Print first `N` Fibonacci numbers
    
3. Find `Nth` Fibonacci number
    
4. Fibonacci using `while` loop
    

---

### 🔹 Intermediate Level

5. Fibonacci using recursion
    
6. Fibonacci using list / array
    
7. Check if a number is Fibonacci
    
8. Sum of first `N` Fibonacci numbers
    

---

### 🔹 Advanced / WOW Level

9. Fibonacci using **dynamic programming**
    
10. Fibonacci using **generator**
    
11. Fibonacci in **O(log n)** (matrix exponentiation – discussion)
    
12. Compare recursion vs iteration time
    
13. Fibonacci without using extra space
    

---

## 🚀 Mini Interview Challenge

`Input: n = 6 Output: 0 1 1 2 3 5`

---

## 🧠 Interview Tip (Golden Answer)

If interviewer asks:

> “Which approach is best?”

Say:

> “Iterative approach is best because it is O(n) time and O(1) space.”

Simple, confident, impressive ⭐