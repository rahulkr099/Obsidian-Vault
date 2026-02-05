# 1.  Given a sequence of numbers. Find all leaders in sequence. An element is a leader if it is strictly greater than all the elements on its right side.
Note:
	 Rightmost element is always a leader.
	 The order of elements in the return sequence must be the same as the given sequence

Example:

The given sequence is 13, 14, 3, 8, 2 .

13 Not a leader because on the right side 14 is greater than 13.
14 lt is a leader because no one greater element in the right side.
3 Not a leader because on the right side 8 are greater than 3.
8 It is a leader because no one greater element on the right side.
2 It is a leader because it is the rightmost element in a sequence.

Hence there are 3 leaders in the above sequence which are 14, 8, 2.
## Answer
## 🔹 What is a Leader?

An element is a **leader** if:
- It is **strictly greater than all elements to its right**
- The **rightmost element is always a leader**
👉 Important:  
The **order of leaders in output must stay the same** as the input.
## 🧠 Key Insight (Smart Thinking)

Instead of checking every element with all elements on the right (which is slow), we can:
### 💡 Scan the array **from right to left**
- Keep track of the **maximum element seen so far**
- If the current element is **greater than max**, it is a leader
- Update max
This works in **O(N)** time (very fast).

---
## ✅ Step-by-Step Approach

1. Start from the **last element**
2. Mark it as leader
3. Move leftwards
4. Compare current element with `max_so_far`
5. If greater → leader
6. Finally reverse the result (to keep original order)

---
## ⏱️ Complexity
- **Time:** `O(N)`
- **Space:** `O(N)` (for storing leaders)


# 2. Given an infinite supply of Indian currency i.e. [1, 2, 5, 10, 20, 50, 100, 500, 1000] valued coins and an amount 'N'.

Find the minimum coins needed to make the sum equal to 'N'. You have to return the list containing the value of coins required in decreasing order.

For Example
For Amount = 70, the minimum number of coins required is 2 i.e an Rs. 50 coin and a Rs. 20 coin.

Note
It is always possible to find the minimum number of coins for the given amount. So, the answer will always exist.

Detailed explanation ( Input/output format, Notes, Images )
Sample Input 1
13
Sample Output 1
10 2 1
Explanation of Sample Input 1
The minimum number of coins to change is 3 {1, 2, 10}.
Sample Input 2
50
Sample Output 2
50

## Answer
## 🧠 Key Idea (Greedy Thinking)

You are given **Indian currency coins**:

`[1, 2, 5, 10, 20, 50, 100, 500, 1000]`

To get the **minimum number of coins**:

- Always take the **largest coin possible first**
- Reduce the amount
- Repeat until the amount becomes `0`

This works perfectly for Indian currency 💯

---
## ✅ Why Greedy Works Here?

Indian coins are designed in such a way that:

- Taking the largest denomination first **always leads to minimum coins**
- There is **no tricky case** where greedy fails

That’s why the problem clearly says:

> “It is always possible to find the minimum number of coins”

---

## 🔁 Step-by-Step Example

### Input

`N = 13`

### Process

- Take `10` → remaining `3`
    
- Take `2` → remaining `1`
    
- Take `1` → remaining `0`
    

### Output

`10 2 1`

Coins are printed in **decreasing order** ✔️

## ⏱️ Complexity

- **Time Complexity:** `O(N)` (worst case when N = 1 repeated)
- **Space Complexity:** `O(N)` (to store coins)

Fast enough for `N ≤ 10^5` ✅

# 3. You have been given three distinct integers ‘X’, ‘Y’ and ‘Z’. You need to find the number with a value in the middle.

For example :

```
X = 4, Y = 6, Z = 2
Here the element with value in the middle is 4, because 2 < 4 < 6.
```

Note :

```
You need to try doing it using minimum comparisons.
```

```python
def middleOfThree(x:int, y:int, z:int):

# Write your code here

# Return an integer

if x < y and x < z:

if y < z:

return y

if z < y:

return z

if y < x and y < z:

if x < z:

return x

if z < x:

return z

if z < x and z < y:

if x < y:

return x

if y < x:

return y
```

 # 4. Shrey has just arrived in the city. When he entered the city, he was given two strings. Now, after arriving at his college, his professor gave him an extra string. To check his intelligence, his professor told him to check if the third string given to him has all the characters of the first and second strings in any order. Help Shrey before his professor scolds him. He has to answer “YES” if all characters are present else “NO”.

```
Example: ‘HELLO’ and ‘SHREY’ are two initial strings, and his professor gave him ’HLOHEELSRY’. So, here all the characters are present, so he has to say “YES”.

Note: The strings contain only uppercase Latin characters.
Detailed explanation ( Input/output format, Notes, Images )
Constraints:

1 <= T <= 10^2
1 <= |FIRST|, |SECOND|, |THIRD| <= 10^5

Time Limit: 1 sec

Sample Input 1:

2
HI HEY EIHYH
ALL GOOD ADOLLG

Sample Output 1:

YES
NO

Explanation For Sample Input 1:

In the first test case, the string ‘THIRD’ has all the characters present in the strings ‘FIRST’ and ‘SECOND’. So, we will return “YES”.

In the second test case, the strings ‘FIRST’ and ‘SECOND’ combined has 1 A, 2 L, 1 G, 2 O and 1 D. While the string ‘THIRD’ has 1 A, 2 L, 1 G, 1 O and 1 D and So, it has one character less than the combined ‘FIRST’ and ‘SECOND’. Thus, we will return “NO”.

Sample Input 1:

2
CODING NINJA NINCODINGJA
YES NO NEEOOYS

Sample Output 1:

YES
NO

Explanation For Sample Input 1:

In the first test case, the string ‘THIRD’ has all the characters present in the strings ‘FIRST’ and ‘SECOND’. So, we will return “YES”.

In the second test case, the strings ‘FIRST’ and ‘SECOND’ combined have 1 N, 1 Y, 1 E, 1 S and 1 O. While the string ‘THIRD’ has 1 N, 1 Y, 2 E, 1 S and 2 O and So, it has one character more than ‘FIRST’ and ‘SECOND’. Thus, we will return “NO”.
```

## 🧠 Key Insight (Very Important)

This is **NOT** about substring  
This is **NOT** about order

This is about **character frequency (count)**.

---

# 🧪 Approach 1: Brute Force (Easy but Slow)

### 💡 Idea

- For every character in FIRST and SECOND
- Try to find and remove it from THIRD
- If at any point a character is missing → NO

---

### 🪜 Steps

1. Convert THIRD string into a list (so we can remove characters)
2. Loop through FIRST:
    - If character exists in THIRD → remove it
    - Else → print NO
3. Loop through SECOND:
    - Same logic
4. If all characters matched → YES

---

### ⏱ Time Complexity
- Worst case: **O(N²)**  
    (Searching and removing again and again)

---

### ❌ Why not good?

- Very slow for large strings (up to 10⁵ length)
- Might fail time limit

---

### ✅ When to use?

- Very small input
- Only for understanding logic

---

# ⚡ Approach 2: Better Solution (Sorting Method)

### 💡 Idea

If THIRD contains exactly all characters of FIRST + SECOND:

👉 Then **sorted(FIRST + SECOND) == sorted(THIRD)**

---

### 🪜 Steps

1. Combine FIRST and SECOND → `COMBINED`
2. Sort `COMBINED`
3. Sort `THIRD`
4. Compare both strings:
    - If same → YES
    - Else → NO


---

### ⏱ Time Complexity

- Sorting takes: **O(N log N)**

---

### ✅ Pros

- Easy to write
- Cleaner logic

### ❌ Cons

- Sorting is still costly
- Not the best for huge inputs

---

### 🧠 Exam Tip

If input size is **medium**, sorting is acceptable.

---

# 🚀 Approach 3: Optimal Solution (Frequency Count) ✅

### 💡 Idea (BEST WAY)

- Count characters using an array of size **26**
- Since only **uppercase letters (A–Z)**

---

### 🪜 Steps

1. Create an array `freq[26]` initialized to 0
2. For each character in FIRST:
    - `freq[char - 'A']++`
3. For each character in SECOND:
    - `freq[char - 'A']++`

4. For each character in THIRD:
    - `freq[char - 'A']--`
5. After this:
    - If **all values in freq[] are exactly 0 → YES**
    - Else → NO

---

### ⏱ Time Complexity

- **O(N)** ✅ (Fastest possible)

### 🧠 Space Complexity

- **O(1)** (Only 26 size array)

---

### 🌟 Why this is BEST?

- Very fast
- Works for large input
- Interview-preferred solution
- Clean and professional

---

## 🧪 Example Walkthrough (Simple)

**FIRST = "ALL"**  
**SECOND = "GOOD"**

Combined counts:

```
A:1 L:2 G:1 O:2 D:1
```

**THIRD = "ADOLLG"**

```
A:1 L:2 G:1 O:1 D:1 ❌ (O is less)
```

So → **NO**

---

## 🧠 Memory Trick (For Exams)

> “Whenever order doesn’t matter → think **frequency array**”

---

## 📌 Final Comparison Table

|Approach|Method|Time|Best For|
|---|---|---|---|
|Brute Force|Remove chars|O(N²)|Learning only|
|Better|Sorting|O(N log N)|Medium input|
|Optimal|Frequency array|O(N)|Exams & Interviews ✅|

---
