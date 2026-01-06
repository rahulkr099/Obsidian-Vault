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
