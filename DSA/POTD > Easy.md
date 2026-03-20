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
Great question—this is a **very common DSA + interview problem** 🔥  
Let’s break it step by step in a clean and simple way.

---

# ✅ Problem Understanding

An element is a **leader** if:  
👉 It is **strictly greater than all elements on its right**

👉 Last element is always a leader

Example:

```
[13, 14, 3, 8, 2]
Leaders → [14, 8, 2]
```

---

# 🧠 1. Brute Force Approach (O(n²))

### 💡 Idea:

For every element, check **all elements on the right**

### 🔁 Steps:

- Pick element `arr[i]`
    
- Compare it with every `arr[j] (j > i)`
    
- If any element is greater → NOT leader
    
- Else → leader
    

### 💻 Code:

```python
def leaders_brute(arr):
    n = len(arr)
    result = []

    for i in range(n):
        is_leader = True
        for j in range(i + 1, n):
            if arr[j] > arr[i]:
                is_leader = False
                break
        
        if is_leader:
            result.append(arr[i])
    
    return result
```

### ⏱ Time Complexity:

- O(n²)
    

---

# 🚀 2. Better Approach (Using Max on Right) — O(n²) but cleaner

### 💡 Idea:

Instead of comparing one by one:

- Use `max(arr[i+1:])`
    

### 💻 Code:

```python
def leaders_better(arr):
    n = len(arr)
    result = []

    for i in range(n):
        if i == n - 1 or arr[i] > max(arr[i+1:]):
            result.append(arr[i])
    
    return result
```

### ⚠️ Note:

- Still O(n²) because `max()` runs each time
    

---

# ⚡ 3. Optimal Approach (Right to Left Scan) — O(n)

### 💡 Best Idea:

Traverse from **right → left**

👉 Keep track of `max_so_far`

- Last element is leader → initialize `max_so_far`
    
- If current element > max_so_far → it's a leader
    
- Update max
    

### 🔁 Steps:

```
Start from end:
2 → leader (max = 2)
8 > 2 → leader (max = 8)
3 < 8 → skip
14 > 8 → leader (max = 14)
13 < 14 → skip
```

### 💻 Code:

```python
def leaders_optimal(arr):
    n = len(arr)
    result = []

    max_so_far = arr[-1]
    result.append(max_so_far)

    for i in range(n - 2, -1, -1):
        if arr[i] > max_so_far:
            result.append(arr[i])
            max_so_far = arr[i]
    
    return result[::-1]   # reverse to maintain order
```

---

# ⏱ Complexity Comparison

|Approach|Time Complexity|Space|
|---|---|---|
|Brute Force|O(n²)|O(1)|
|Better (max)|O(n²)|O(1)|
|Optimal|O(n)|O(n)|

---

# 🧠 Interview Tip (Very Important 🚨)

When explaining:  
👉 Start with brute → then optimize  
👉 Say this line:

💬  
_"Instead of checking every element on the right repeatedly, we can traverse from right and keep track of maximum. This reduces time complexity to O(n)."_

---

# 💡 Bonus Idea (Level Up 🚀)

Try these variations:

- Count number of leaders
    
- Return indices instead of values
    
- Find leaders in **circular array**
    

---

If you want, I can turn this into a **perfect interview answer script** or give you **LeetCode-style variations** 🔥


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

Great — you already understood the **greedy idea perfectly** 👍  
Now let’s turn that into clean, interview-ready Python code.

---

## ✅ Python Code (Greedy Approach)

```python
def min_coins(N):
    coins = [1000, 500, 100, 50, 20, 10, 5, 2, 1]  # decreasing order
    result = []

    for coin in coins:
        while N >= coin:
            result.append(coin)
            N -= coin

    return result
```

---

## 🔍 Example Run

```python
print(min_coins(13))
```

### Output:

```python
[10, 2, 1]
```

---

## ⚡ Better Optimized Version (Interview Upgrade)

Instead of using `while`, we can directly calculate how many coins we need.

```python
def min_coins(N):
    coins = [1000, 500, 100, 50, 20, 10, 5, 2, 1]
    result = []

    for coin in coins:
        count = N // coin   # how many times this coin fits
        if count > 0:
            result.extend([coin] * count)
            N -= coin * count

    return result
```

---

## 🔥 Why this version is better?

- No repeated subtraction
    
- Faster in practice
    
- Cleaner logic (interviewers love this)
    

---

## 🧠 Dry Run (N = 70)

|Coin|Count|Remaining|
|---|---|---|
|50|1|20|
|20|1|0|

👉 Result:

```python
[50, 20]
```

---

## 🚀 Pro Tip (Very Important for Interviews)

Whenever you see:

- Coins / denominations
    
- Minimum number of coins
    
- "Always possible" condition
    

👉 Immediately think:

```text
GREEDY + largest first
```

---

If you want next level:  
I can show you **where greedy FAILS** and you must use **DP (coin change problem)** — that’s a very powerful concept for interviews 🔥

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

 #  4. Shrey has just arrived in the city. When he entered the city, he was given two strings. Now, after arriving at his college, his professor gave him an extra string. To check his intelligence, his professor told him to check if the third string given to him has all the characters of the first and second strings in any order. Help Shrey before his professor scolds him. He has to answer “YES” if all characters are present else “NO”.

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
# 5. You are given a string 'S' of length 'N' consisting of lowercase English alphabet letters. You are also given a positive integer 'K'. Now, a substring of this string is good if it contains at most 'K' distinct characters. A string 'X' is a substring of string 'Y' if it can be obtained by deletion of several continuous elements(possibly zero) from the beginning and the end from the string 'Y'. Your task is to return the maximum size of any good substring of the string 'S'.

**Example:**

```
‘S’ = “bacda” and ‘K’ = 3.

So, the substrings having at most ‘3’ distinct characters are called good substrings. Some possible good substrings are:
1. “bac”
2. “acd”
3. “acda”

The substring “acda” is the largest possible good substring, as we cannot get any other substring of length 5 or more having distinct characters less than or equal to ‘3’. Thus, you should return ‘4’ as the answer.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 10
1 <= K <= 26
1 <= N <= 10^4

All the characters of the string are lowercase English alphabet letters.

Time Limit: 1 sec
```

**Sample Input 1:**

```
2
2
abcbc
1
abccc
```

**Sample Output 1:**

```
4
3
```

**Explanation For Sample Input 1:**

```
For the first test case :
K = 2, so we can choose substring “bcbc” having 2 distinct character which is less than or equal to K = 2. 

We cannot get any other substring of length 5 or more having distinct characters less than or equal to 2. Thus, you should return ‘4’ as the answer.

For the second test case :
K = 1, so we can choose substring “ccc” having only 1 distinct character which is less than or equal to K = 1. 

We cannot get any other substring of length 4 or more having distinct characters less than or equal to 1. Thus, you should return ‘3’ as the answer.
```

**Sample Input 2:**

```
1
6
abcba
3
acbdab
```

**Sample Output 2:**

```
5
4
```

Nice problem 👍  
This is a **very famous sliding window problem**. I’ll explain it **slowly**, in **simple words**, and in **three levels**:

1. Brute Force
    
2. Better Solution
    
3. Optimal Solution (Sliding Window) ✅
    

I’ll also give **Python code** for each so you can clearly see the difference.

---

## 🔍 Problem Restated (Very Simple)

You are given:

- A string **S**
    
- A number **K**
    

👉 A substring is **good** if it has **at most K distinct characters**.

Your goal:

> **Find the maximum length of any good substring**

---

## 🧠 Key Observation (IMPORTANT)

- “At most K” means **≤ K**
    
- Order must be **continuous** (substring, not subsequence)
    
- We must try **all possible substrings** and pick the **longest valid one**
    

---

# 🧪 1. Brute Force Solution (Easy but Slow)

### 💡 Idea

- Generate **all substrings**
    
- For each substring:
    
    - Count distinct characters
        
    - If distinct ≤ K → update answer
        

---

### 🪜 Steps

1. Fix starting index `i`
    
2. Fix ending index `j`
    
3. Extract substring `S[i:j+1]`
    
4. Count distinct characters using `set`
    
5. Track maximum length
    

---

### 🧑‍💻 Python Code (Brute Force)

```python
def max_good_substring_bruteforce(s, k):
    n = len(s)
    ans = 0

    for i in range(n):
        for j in range(i, n):
            substring = s[i:j+1]
            if len(set(substring)) <= k:
                ans = max(ans, j - i + 1)

    return ans
```

---

### ⏱ Time Complexity

- Substrings: `O(N²)`
    
- Set operation: `O(N)`
    
- ❌ Overall: `O(N³)`
    

---

### ❌ Why not good?

- Too slow for large `N`
    
- Only useful to **understand logic**
    

---

# ⚡ 2. Better Solution (Improved Brute Force)

### 💡 Idea

Instead of recalculating `set()` every time:

- Use a **frequency array**
    
- Extend substring from `i`
    
- Stop when distinct characters exceed `K`
    

---

### 🪜 Steps

1. Fix starting index `i`
    
2. Create frequency array of size 26
    
3. Move `j` forward:
    
    - Update frequency
        
    - Track distinct count
        
4. If distinct > K → break
    

---

### 🧑‍💻 Python Code (Better)

```python
def max_good_substring_better(s, k):
    n = len(s)
    ans = 0

    for i in range(n):
        freq = [0] * 26
        distinct = 0

        for j in range(i, n):
            idx = ord(s[j]) - ord('a')
            if freq[idx] == 0:
                distinct += 1
            freq[idx] += 1

            if distinct > k:
                break

            ans = max(ans, j - i + 1)

    return ans
```

---

### ⏱ Time Complexity

- `O(N²)` ✅  
    Much better than brute force
    

---

### ✅ When to use?

- Medium constraints
    
- Exam-friendly improvement
    

---

# 🚀 3. Optimal Solution (Sliding Window) ✅

### 💡 Core Idea (BEST)

Use **two pointers (sliding window)**:

- Expand window using `right`
    
- Shrink window using `left` when distinct > K
    

👉 Window always stays **valid**

---

### 🪜 Steps

1. Initialize:
    
    - `left = 0`
        
    - `freq[26]`
        
    - `distinct = 0`
        
2. Move `right` pointer:
    
    - Add character
        
3. If `distinct > K`:
    
    - Move `left` pointer
        
    - Remove characters
        
4. Update maximum length
    

---

### 🧑‍💻 Python Code (Optimal)

```python
def max_good_substring_optimal(s, k):
    n = len(s)
    freq = [0] * 26
    left = 0
    distinct = 0
    ans = 0

    for right in range(n):
        idx = ord(s[right]) - ord('a')
        if freq[idx] == 0:
            distinct += 1
        freq[idx] += 1

        while distinct > k:
            left_idx = ord(s[left]) - ord('a')
            freq[left_idx] -= 1
            if freq[left_idx] == 0:
                distinct -= 1
            left += 1

        ans = max(ans, right - left + 1)

    return ans
```

---

### ⏱ Time Complexity

- **O(N)** ✅  
    (each character added & removed once)
    

### 🧠 Space Complexity

- **O(1)** (26 characters only)
    

---

## 🧪 Example Walkthrough

**S = "abcbc", K = 2**

Sliding window finds:

```
"bcbc" → length 4 ✅
```

---

## 📊 Comparison Table

|Approach|Time|Space|Recommended|
|---|---|---|---|
|Brute Force|O(N³)|O(N)|❌ No|
|Better|O(N²)|O(1)|⚠️ Okay|
|Sliding Window|O(N)|O(1)|✅ BEST|

---

## 🧠 Memory Trick (Very Useful)

> **Substring + condition + max/min → think SLIDING WINDOW**

---

# 6. Given a string ‘STR’ consisting of lower case English letters, the task is to find the first non-repeating character in the string and return it. If it doesn’t exist, return ‘#’.

For example:

```
For the input string 'abcab', the first non-repeating character is ‘c’. As depicted the character ‘a’ repeats at index 3 and character ‘b’ repeats at index 4. Hence we return the character ‘c’ present at index 2.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 100
1 <= N <= 10 ^ 4

Where ‘T’ is the number of test cases, and ‘N’ is the length of the string.

Time Limit: 1 sec
```

**Sample Input 1:**

```
2
bbabcbcb
babaabea
```

**Sample Output 1:**

```
a
e
```

**Explanation of Sample Input 1:**

```
For the first test case, 
the first non-repeating character is ‘a’. As depicted the character ‘b’ repeats at index 1, 3, 5, 7, and character ‘c’ repeats at index 6. Hence we return the character ‘a’ present at index 2.

For the second test case, 
the character ‘e’ is the first non-repeating character. As depicted the character ‘b’ repeats at index 2, 5, and character ‘a’ repeats at index 3, 4, and 7. Hence we return the character ‘e’ present at index 6.
```

**Sample Input 2:**

```
3
cbbd
bebeeed
abcd
```

**Sample Output 2:**

```
c
d
a
```

Great problem 👍 This one is **very common in exams, interviews, and coding practice**.  
Let’s solve it **step by step**, from simple to best.

I’ll explain in **easy words** and give **Python code** (you can easily convert to C++/Java later).

---

# 🧠 Problem in one line

For each string, **find the first character that appears only once**.  
If no such character exists → return `#`.

---

## 🟢 1️⃣ Brute Force Solution (Very simple, slow)

### 👉 Idea

For every character:

- Count how many times it appears in the whole string
    
- If count == 1 → return it
    

### ⏱ Time Complexity

- For each character (N), we scan the string (N)
    
- **O(N²)** ❌ (slow for large input)
    

### 🧾 Space Complexity

- **O(1)**
    

### ✅ Python Code

```python
def firstNonRepeating_bruteforce(s):
    for i in range(len(s)):
        count = 0
        for j in range(len(s)):
            if s[i] == s[j]:
                count += 1
        if count == 1:
            return s[i]
    return '#'
```

### ✔ Example

```
"abcab" → c
```

---

## 🟡 2️⃣ Better Solution (Using frequency array)

### 👉 Idea

- Count frequency of each character first
    
- Then scan string again to find first char with frequency 1
    

Since only **lowercase letters**, we use array of size 26.

### ⏱ Time Complexity

- Counting → O(N)
    
- Checking → O(N)
    
- **Total: O(N)** ✅
    

### 🧾 Space Complexity

- **O(26) → O(1)**
    

### ✅ Python Code

```python
def firstNonRepeating_better(s):
    freq = [0] * 26

    for ch in s:
        freq[ord(ch) - ord('a')] += 1

    for ch in s:
        if freq[ord(ch) - ord('a')] == 1:
            return ch

    return '#'
```

### ✔ Example

```
"bbabcbcb" → a
```

---

## 🔵 3️⃣ Optimal Solution (Using dictionary / hashmap)

### 👉 Idea

- Use a hashmap (dictionary) to count characters
    
- Preserve order by scanning string again
    

This is **clean, readable, and interview-friendly**.

### ⏱ Time Complexity

- **O(N)** ✅
    

### 🧾 Space Complexity

- **O(N)** (worst case all characters unique)
    

### ✅ Python Code

```python
def firstNonRepeating_optimal(s):
    freq = {}

    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1

    for ch in s:
        if freq[ch] == 1:
            return ch

    return '#'
```

---

## 🧪 Handling Multiple Test Cases

```python
t = int(input())
for _ in range(t):
    s = input().strip()
    print(firstNonRepeating_optimal(s))
```

---

## 📊 Comparison Summary

|Approach|Time|Space|Use when|
|---|---|---|---|
|Brute Force|O(N²)|O(1)|Learning basics|
|Better (Array)|O(N)|O(1)|Exams, constraints known|
|Optimal (Map)|O(N)|O(N)|Interviews, clean code|

---

## 💡 Pro Tip (Exam & Interview)

- **Mention brute force first**
    
- Then improve it
    
- End with optimal → interviewer loves this flow 😄
    

---

If you want next:

- C++ / Java version
    
- Interview explanation in words
    
- Similar problems for practice
    
- Dry run with diagram
    

Just tell me 🚀

# Given the time in hours and minutes, you need to calculate the angle between the hour hand and the minute hand.

**Note :**

```
There can be two angles between the hour hand and minute hand, you need to print a minimum of two. Also, print the floor value of angle i.e. if the angle is 15.2, you need to print 15.
```
**Constraints:**

```
1 <= T <= 50
1 <= H <= 12
0 <= M <= 59

Time Limit: 1 sec
```

##### Sample Input 1:

```
2
6 30
8 55
```

##### Sample Output 1:

```
15
62
```

##### Explanation For Sample Input 1:

```
For test case 1: when the time is 6:30 the two angles between the hour hand and the minute hand is 15 degree and 345 degrees. As 15 is the smallest so the ans is 15.

For test case 1: when the time is 8:55 the two angles between the hour hand and the minute hand is 62.5 degree and 297.5 degrees. As 62.75 is the smallest so the ans is 62.
```

##### Sample Input 2:

```
2
3 30
12 0
```

##### Sample Output 2:

```
75
0
```

Nice problem 👍—this one is very common in exams and interviews, so learning it **step by step** is a great idea.

We’ll solve it in **three ways**:

1. Brute force
    
2. Better
    
3. Optimal (best + clean formula)
    

I’ll keep words simple and logic very clear.

---

## 🕒 Basic idea (important to understand first)

- A **clock has 360°**
    
- **Hour hand**
    
    - Moves **30° per hour** (360 ÷ 12)
        
    - Also moves **0.5° per minute** (30 ÷ 60)
        
- **Minute hand**
    
    - Moves **6° per minute** (360 ÷ 60)
        

After finding positions of both hands:

- Take the **absolute difference**
    
- Choose the **minimum angle**
    
- Print the **floor value**
    

---

## 1️⃣ Brute Force Approach (Slow but easy to understand)

### Idea

Simulate how much each hand moves from 12:00.

### Steps

1. Hour hand movement:
    
    - `hour_angle = (H % 12) * 30 + M * 0.5`
        
2. Minute hand movement:
    
    - `minute_angle = M * 6`
        
3. Find difference:
    
    - `angle = abs(hour_angle - minute_angle)`
        
4. Minimum angle:
    
    - `angle = min(angle, 360 - angle)`
        
5. Print `floor(angle)`
    

### Code (Brute Force)

```python
import math

def clock_angle_bruteforce(H, M):
    hour_angle = (H % 12) * 30 + M * 0.5
    minute_angle = M * 6

    angle = abs(hour_angle - minute_angle)
    angle = min(angle, 360 - angle)

    return math.floor(angle)
```

✔ Easy  
❌ Slightly repetitive calculations

---

## 2️⃣ Better Approach (Cleaner logic)

### Improvement

Same math, but we **directly think in angles**, no simulation feeling.

### Formula

```
angle = |30H - 5.5M|
```

Why?

- Hour hand = `30H + 0.5M`
    
- Minute hand = `6M`
    
- Difference = `|30H + 0.5M - 6M|`
    
- Simplify → `|30H - 5.5M|`
    

### Code (Better)

```python
import math

def clock_angle_better(H, M):
    angle = abs(30 * H - 5.5 * M)
    angle = min(angle, 360 - angle)
    return math.floor(angle)
```

✔ Short  
✔ Faster  
✔ Interview-friendly

---

## 3️⃣ Optimal Approach (Best & standard)

### Why this is optimal?

- O(1) time
    
- O(1) space
    
- Direct formula
    
- Clean and professional
    

### Final Formula

```
min(|30H - 5.5M|, 360 - |30H - 5.5M|)
```

### Code (Optimal)

```python
import math

def clock_angle_optimal(H, M):
    angle = abs(30 * (H % 12) - 5.5 * M)
    return math.floor(min(angle, 360 - angle))
```

✔ Best for exams  
✔ Best for interviews  
✔ Best for competitive programming

---

## 🧪 Example Walkthrough

### Input: `8 55`

- `|30×8 - 5.5×55|`
    
- `|240 - 302.5| = 62.5`
    
- Minimum = `62.5`
    
- Floor → **62**
    

✔ Output matches sample

---

## 🚀 Extra Tips (for improvement)

- Memorize this formula: **`|30H - 5.5M|`**
    
- Always apply **`min(angle, 360 - angle)`**
    
- Don’t forget **floor value**
    
- Use `(H % 12)` to avoid errors for 12
    

---

If you want, next I can:

- Convert this to **C / C++ / Java**
    
- Give **trick to remember formula**
    
- Provide **exam-ready short answer**
    
- Give **MCQs based on this concept**
    

Just tell me 😊

# You are provided with the two strings named X and Y respectively. Y has its own specific order and has no repeating characters. Your task is to arrange the characters of the first string i.e. X in such a way that the order of characters in X is exactly the same as in Y, which means if ‘d’ occurs after ‘c’ in Y then it should also occur after ‘c’ in X ( obviously if X has ‘d’ and ‘c’ as characters in it ). All you have to do is, convert string X in the specific order with respect to string Y.

Note :

```
Both the strings have only lowercase English alphabets. 
There may be more than one correct solution, you have to return any one of the possible solutions.
```

**Constraints :**

```
1 <= T <= 10
1 <= |X| <= 10000
1 <= |Y| <= 26
where ‘T’ is the number of test cases, |X| is the length of the first string and |Y| is the length of the second string.
Time Limit: 1 sec
```

#### Sample Input 1:

```
1
acabd
abc
```

#### Sample Output 1:

```
aabcd
```

#### Explanation of Sample Input 1:

```
String Y has ‘a’ first then ‘b’ and then ‘c’ and therefore string X must be ordered as ‘aabcd’ to keep the respective order of characters same as in string Y.
Other possible answers are: ‘daabc’ , ‘adabc’ , ‘aadbc’, ‘aabdc’.
```

#### Sample Input 2:

```
4
dfhfgk
h
aabbb
gd
abababab
ab
cag
abcdef
```

#### Sample Output 2:

```
hdffgk
aabbb
aaaabbbb
acg
```

Nice, this is a **classic ordering problem**.  
Let’s solve it in **three levels** so you clearly see how to improve step by step 👇  
I’ll keep the words simple and exam-friendly.

---

# 🔹 Problem recap (in one line)

You must **rearrange string X** so that characters appear in the **same relative order as in Y**.  
Characters not present in Y can be placed anywhere.

---

# 🥉 1️⃣ Brute Force Solution

(Simple but slow – good for understanding)

### 💡 Idea

- For each character in **Y**
    
- Scan the whole **X**
    
- Pick matching characters
    
- Then pick remaining characters
    

### ❌ Drawback

- Repeated scanning
    
- Slow for large strings
    

### ⏱️ Time Complexity

```
O(|X| × |Y|)
```

---

### ✅ Brute Force Code

```python
def specificOrder_bruteforce(X, Y):
    result = []
    used = [False] * len(X)

    # Place characters in Y order
    for ch in Y:
        for i in range(len(X)):
            if X[i] == ch and not used[i]:
                result.append(ch)
                used[i] = True

    # Place remaining characters
    for i in range(len(X)):
        if not used[i]:
            result.append(X[i])

    return ''.join(result)
```

---

# 🥈 2️⃣ Better Solution

(Using sorting + custom priority)

### 💡 Idea

- Give each character a **priority**
    
- Characters in Y get higher priority
    
- Sort X based on that priority
    

### ⏱️ Time Complexity

```
O(|X| log |X|)
```

### 🧠 Why better?

- Cleaner
    
- No nested loops
    
- Still not optimal
    

---

### ✅ Better Solution Code

```python
def specificOrder_better(X, Y):
    priority = {}

    # Assign priority based on Y
    for i in range(len(Y)):
        priority[Y[i]] = i

    # Characters not in Y get large priority
    def sort_key(ch):
        return priority[ch] if ch in priority else len(Y)

    return ''.join(sorted(X, key=sort_key))
```

---

# 🥇 3️⃣ Best Solution (Optimal)

(Frequency counting – fastest & cleanest)

### 💡 Idea

- Count frequency of characters in X
    
- Add characters in order of Y
    
- Add remaining characters
    

### ⏱️ Time Complexity

```
O(|X| + |Y|)
```

### 🧠 Why BEST?

- No sorting
    
- No nested loops
    
- Works fast even for 10,000 characters
    

---

### ✅ Best Solution Code (Recommended)

```python
def specificOrder_best(X, Y):
    freq = [0] * 26

    # Count characters in X
    for ch in X:
        freq[ord(ch) - ord('a')] += 1

    result = []

    # Add characters in Y order
    for ch in Y:
        idx = ord(ch) - ord('a')
        if freq[idx] > 0:
            result.append(ch * freq[idx])
            freq[idx] = 0

    # Add remaining characters
    for i in range(26):
        if freq[i] > 0:
            result.append(chr(i + ord('a')) * freq[i])

    return ''.join(result)
```

---

# 📊 Comparison Table (very useful for exams)

|Approach|Time Complexity|Space|Verdict|
|---|---|---|---|
|Brute Force|O(X × Y)|O(X)|❌ Slow|
|Better|O(X log X)|O(X)|👍 Good|
|Best|O(X + Y)|O(1)|⭐ Best|

---

# 🚀 Final exam tip

If asked:

> _“Write the most efficient solution”_

👉 Always choose **frequency-count method**  
👉 Mention **O(n)** time complexity

You’re thinking in the **right direction** 👏  
If you want, I can:

- Add **dry run**
    
- Convert to **C / Java**
    
- Write **exam-style explanation**
    
- Handle **T test cases**
    

Just tell me 😊

# You are given a string 'STR'. The string contains [a-z] [A-Z] [0-9] [special characters]. You have to find the reverse of the string.

For example:

```
 If the given string is: STR = "abcde". You have to print the string "edcba".
```

**follow up:**

```
Try to solve the problem in O(1) space complexity. 
```
**Constraints:**

```
1 ≤ T ≤ 10
1 ≤ |STR| ≤ 10 ^ 5 

Where |STR| is the length of the string STR.

Time limit: 1 sec.
```

##### Sample Input 1:

```
3
abcde
coding
hello1
```

##### Sample Output 1:

```
edcba
gnidoc
1olleh
```

##### Explanation of the Sample Input 1:

```
For the first test case, STR = "abcde". We need to reverse the string, that is the first element becomes the last element and the last element becomes the first element, the second element becomes the second last element and the second last element becomes the second element and so on. So we get, "edcba".
```

##### Sample Input 2:

```
3
a
1det@Z
$1xYuP
```

##### Sample Output 2

```
a
Z@ted1
PuYx1$
```

Great question 👍 This is a classic string problem, but the **O(1) space follow-up** makes it more interesting.

We’ll solve it in 3 ways:

- ✅ Brute Force
    
- ✅ Better
    
- ✅ Optimal (O(1) extra space)
    

---

# 🔹 1️⃣ Brute Force Solution

### 💡 Idea:

Create a new string and append characters from the end to the start.

### ⏱ Time Complexity: O(N)

### 📦 Space Complexity: O(N) (extra string used)

### ✅ Python Code:

```python
def reverse_string_brute(s):
    result = ""
    for i in range(len(s) - 1, -1, -1):
        result += s[i]
    return result
```

### ⚠ Problem:

String concatenation inside loop is costly (strings are immutable in Python).  
It creates many intermediate strings.

---

# 🔹 2️⃣ Better Solution

### 💡 Idea:

Convert string to list, reverse using slicing.

### ⏱ Time Complexity: O(N)

### 📦 Space Complexity: O(N)

### ✅ Python Code:

```python
def reverse_string_better(s):
    return s[::-1]
```

OR

```python
def reverse_string_better(s):
    return ''.join(reversed(s))
```

### ✔ Why better?

Cleaner, faster than manual concatenation.

But still uses **extra space**.

---

# 🔹 3️⃣ Optimal Solution (O(1) Space) 🔥

Now this is what interviewers love.

### 💡 Idea:

Use **two-pointer swapping**.  
Convert string into list (since Python strings are immutable).  
Swap from start and end moving inward.

### ⏱ Time Complexity: O(N)

### 📦 Extra Space: O(1)

(Only constant variables used. We modify in-place.)

---

### ✅ Python Code:

```python
def reverse_string_optimal(s):
    arr = list(s)   # convert to list to allow modification
    left = 0
    right = len(arr) - 1

    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

    return ''.join(arr)
```

---

# 🔹 How It Works (Example: "hello1")

Initial:

```
h e l l o 1
^         ^
```

Swap:

```
1 e l l o h
  ^     ^
```

Swap:

```
1 o l l e h
    ^ ^
```

Done ✅

Result: `"1olleh"`

---

# 🚀 If You Want Truly O(1) Space

In languages like **C++**, you can directly modify the string without converting:

```cpp
void reverseString(string &s) {
    int left = 0;
    int right = s.length() - 1;

    while(left < right) {
        swap(s[left], s[right]);
        left++;
        right--;
    }
}
```

That is **real in-place reversal**.

---

# 🔥 Final Comparison

|Approach|Time|Space|Good For|
|---|---|---|---|
|Brute Force|O(N)|O(N)|Basic understanding|
|Slicing|O(N)|O(N)|Clean coding|
|Two Pointer|O(N)|O(1)|Interviews 🔥|

---

# 💡 Pro Tip (Interview Ready)

If interviewer asks:

> “Can you do this without extra space?”

You should immediately think:  
👉 Two pointers  
👉 In-place swapping  
👉 Left & Right movement

---

If you want, I can also give:

- Java version
    
- C version
    
- Competitive programming input format version
    
- Or how to handle multiple test cases properly
    

Just tell me 😄




# You are given an array/list ‘ARR’ of size ‘N’. ‘ARR' is binary i.e. it contains only 0s and 1s (ARR[i] = {0, 1}). Your task is to find out the minimum number of swaps required to group all 1s together.

Note: If ‘ARR’ contains only 0’s then print -1.

Example:

```
Let ‘ARR’ = [ 0, 1, 0, 1]. We can group all 1s together in the following ways: ‘ARR’ =[0, 0, 1, 1] or ‘ARR’ = [0, 1, 1, 0]. 

In this example, we need only 1 swap to group all 1’s together which is the minimum possible. 
```

**Constraints:**

```
1 <= ‘T’ <= 100
2 <= ‘N’ <= 5000
0 <= ‘ARR[i]’ <= 1

Where ‘ARR[i]’ represents the elements of array/list ‘ARR’. 

Time Limit: 1 sec
```

##### Sample Input 1:

```
2
5
1 0 1 0 1
6
1 1 1 1 1 1
```

##### Sample Output 1:

```
1
0
```

#### Explanation for Sample Output 1:

```
In test case 1, swap ‘ARR[1]’ and ‘ARR[4]’ (0-based indexing). Then ‘ARR’ = [1, 1, 1, 0, 0]. So, the minimum swaps to group all 1s together is 1.

In test case 2, all 1s are already together in 'ARR'. So, we don’t need any swaps. Hence, the minimum swaps to group all 1s together is 0.
```

##### Sample Input 2:

```
2
4 
0 0 0 0
6
1 1 0 0 1 1
```

##### Sample Output 2:

```
-1
 2
```

#### Explanation for Sample Output 2:

```
In test case 1, the number of 1s in 'ARR' is 0. So we return -1.

In test case 2, first, we swap ‘ARR[2]’ and ‘ARR[4]’ (0-based indexing). Now, ‘ARR’ = [1, 1, 1, 0, 0, 1].
Then, swap ‘ARR[3]’ and ‘ARR[5]’. Now, ‘ARR’ = [1, 1, 1, 1, 0, 0]. So, the minimum swaps to group all 1s together is 2.
```

Nice problem! Let’s break it down step-by-step and build intuition first, then move from **brute → better → optimal** solutions.

---

# 🧠 Problem Understanding

You need to **group all 1s together** with **minimum swaps**.

Important observations:

- Order doesn’t matter.
    
- Swapping can be between any two positions.
    
- Goal = all 1s should be **contiguous**.
    
- If array has **no 1s → return -1**.
    

---

# 🔎 Key Insight (Core Logic)

If total number of `1`s = **k**

Then all valid grouped arrangements must contain a block (window) of size **k** that holds all 1s.

👉 So we just need to find:

> A window of size **k** having **maximum number of 1s**

Why?

Because:

```
swaps needed = k − (number of 1s already inside window)
```

We want swaps minimum → maximize ones inside window.

---

# 🥉 1. Brute Force Solution

### Idea

Check every possible window of size `k` and count how many 1s inside.

### Steps

1. Count total 1s → `k`
    
2. For each window of size k:
    
    - count 1s
        
    - calculate swaps
        
3. Take minimum.
    

---

### Complexity

- Time = **O(N²)**
    
- Space = O(1)
    

---

### Code

```python
def min_swaps_bruteforce(arr):
    k = arr.count(1)
    if k == 0:
        return -1

    n = len(arr)
    ans = float('inf')

    for i in range(n - k + 1):
        ones = 0
        for j in range(i, i + k):
            if arr[j] == 1:
                ones += 1

        ans = min(ans, k - ones)

    return ans
```

---

# 🥈 2. Better Solution (Prefix Sum)

Instead of counting ones again and again, precompute prefix sums.

### Idea

Prefix array stores count of 1s till index.

Then window ones count:

```
ones = prefix[r] - prefix[l-1]
```

---

### Complexity

- Time = **O(N)**
    
- Space = **O(N)**
    

---

### Code

```python
def min_swaps_better(arr):
    k = arr.count(1)
    if k == 0:
        return -1

    n = len(arr)

    prefix = [0]*n
    prefix[0] = arr[0]

    for i in range(1,n):
        prefix[i] = prefix[i-1] + arr[i]

    ans = float('inf')

    for i in range(n-k+1):
        j = i + k - 1
        ones = prefix[j] - (prefix[i-1] if i>0 else 0)
        ans = min(ans, k - ones)

    return ans
```

---

# 🥇 3. Optimal Solution (Sliding Window) 🚀

This is the best solution and interview favorite.

---

### Idea

Instead of recomputing counts, maintain a sliding window of size `k`.

When window moves:

- subtract outgoing element
    
- add incoming element
    

---

### Complexity

- Time = **O(N)**
    
- Space = **O(1)** ✅
    

---

### Code

```python
def min_swaps_optimal(arr):
    k = arr.count(1)
    if k == 0:
        return -1

    n = len(arr)

    # count ones in first window
    ones = sum(arr[:k])
    max_ones = ones

    for i in range(k, n):
        ones += arr[i]      # add new
        ones -= arr[i-k]    # remove old
        max_ones = max(max_ones, ones)

    return k - max_ones
```

---

# 🔥 Example Walkthrough

```
arr = [1,0,1,0,1]
k = 3
```

Windows size = 3

|Window|Ones|Swaps|
|---|---|---|
|[1,0,1]|2|1|
|[0,1,0]|1|2|
|[1,0,1]|2|1|

Minimum = **1**

---

# 🏆 Final Complexity Comparison

|Approach|Time|Space|Notes|
|---|---|---|---|
|Brute|O(N²)|O(1)|slow|
|Prefix|O(N)|O(N)|faster|
|Sliding|O(N)|O(1)|best ⭐|

---

# 🎯 Interview Answer Summary (Short Form)

If asked directly:

> Count total 1s = k.  
> Use sliding window of size k.  
> Find window with max 1s.  
> Answer = k − maxOnes.

---

# 💡 Advanced Thought (Bonus Insight)

Same trick works for:

- grouping all 0s together
    
- minimum swaps to group characters
    
- grouping vowels together
    
- grouping same values
    

This pattern is called:

> **Fixed-size Sliding Window Optimization**

---

If you want, I can also show a visual animation style dry run to make this idea instantly intuitive.
