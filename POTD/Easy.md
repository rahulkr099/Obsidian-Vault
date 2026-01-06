1.  Given a sequence of numbers. Find all leaders in sequence. An element is a leader if it is strictly greater than all the elements on its right side.
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