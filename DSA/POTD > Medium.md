# 1. You are given a string ‘STR’ consisting of lowercase English alphabets. Your take is to find out the minimum number of character deletions required such that each character in the final string has a unique frequency.

Detailed explanation ( Input/output format, Notes, Images )![[Pasted image 20260106204848.png]]
## 🧠 Core Idea (Very Important)

1. Count frequency of each character
    
2. Keep a **set** of used frequencies
    
3. If a frequency is already used:
    
    - Keep deleting (reduce frequency)
        
    - Until it becomes unused or zero
        
4. Count how many deletions you did
    

This greedy approach guarantees **minimum deletions**.

# 2. You are given a binary tree. Return the count of unival sub-trees in the given binary tree. In unival trees, all the nodes, below the root node, have the same value as the data of the root.

For example: for the binary tree, given in the following diagram, the number of unival trees is 5.

![[Pasted image 20260205210343.png]]
**Constraints:**

```
1 <= T <= 10
0 <= N <= 10^5
0 <= data <= 10^4, where data is the value for a node.

Time Limit: 1sec
```

##### Sample Input 1:

```
1 1 1 -1 -1 -1 -1
```

##### Sample Output 1:

```
3
```

##### Sample Input 2:

```
1 2 3 2 -1 3 4 -1 -1 3 3 -1 -1 -1 -1 -1 -1
```

##### Sample Output 2:

```
6
```

##### Explanation to Sample Input 2:

```
The input binary tree will be represented as 
``` 
![[Pasted image 20260205210436.png]]
```
In the above diagram, the orange marked nodes are the root nodes of the unival sub-trees for the given binary tree.
```

Great problem 👍  
This is a **classic binary tree recursion problem**. I’ll explain it **clearly**, in **simple words**, and in **three levels**:

1. Brute Force
    
2. Better Solution
    
3. Optimal Solution (Post-order recursion) ✅
    

I’ll also give **Python code that fits exactly into your given template**.

---

## 🌳 What is a Unival (Universal Value) Subtree?

A subtree is **unival** if:

- All nodes in that subtree have **the same value**
    

✅ **Single node** is always a unival subtree.

---

## 🧠 Key Insight (Very Important)

- Leaf nodes → always unival
    
- Bigger subtree → unival **only if**
    
    - Left subtree is unival
        
    - Right subtree is unival
        
    - Root value == left child value (if exists)
        
    - Root value == right child value (if exists)
        

---

# 🧪 1. Brute Force Solution (Very Slow)

### 💡 Idea

For **every node**:

1. Check if its subtree is unival
    
2. Count it if yes
    

---

### 🪜 Steps

- For each node:
    
    - Traverse entire subtree
        
    - Verify all values are same
        

---

### ⏱ Time Complexity

❌ **O(N²)**  
(each node checks its subtree again)

---

### 🧑‍💻 Brute Force Code

```python
def isUnival(root, value):
    if root is None:
        return True
    if root.data != value:
        return False
    return isUnival(root.left, value) and isUnival(root.right, value)


def countUnivalTrees(root):
    if root is None:
        return 0

    count = countUnivalTrees(root.left) + countUnivalTrees(root.right)

    if isUnival(root, root.data):
        count += 1

    return count
```

---

### ❌ Why not good?

- Repeated traversal
    
- Too slow for large trees
    

---

# ⚡ 2. Better Solution (Top-Down with Flags)

### 💡 Idea

- Along with counting, return **whether subtree is unival**
    
- Avoid rechecking full subtree
    

---

### 🪜 Steps

- Recursive function returns:
    
    - `(is_unival, count)`
        

---

### ⏱ Time Complexity

⚠️ **O(N)**  
Better, but logic slightly complex

---

### 🧑‍💻 Better Solution Code

```python
def helper(root):
    if root is None:
        return True, 0

    left_unival, left_count = helper(root.left)
    right_unival, right_count = helper(root.right)

    total = left_count + right_count

    if not left_unival or not right_unival:
        return False, total

    if root.left and root.left.data != root.data:
        return False, total

    if root.right and root.right.data != root.data:
        return False, total

    return True, total + 1


def countUnivalTrees(root):
    return helper(root)[1]
```

---

# 🚀 3. Optimal Solution (Post-Order Traversal) ✅

### 💡 Core Idea (BEST)

- Use **post-order traversal**
    
- Count while returning **is_unival status**
    
- Each node processed **once**
    

---

### 🪜 Steps

1. Traverse left
    
2. Traverse right
    
3. Decide if current subtree is unival
    
4. Increment count if yes
    

---

### ⏱ Time Complexity

✅ **O(N)**

### 🧠 Space Complexity

✅ **O(H)** (recursion stack)

---

## ✅ FINAL OPTIMAL CODE (Fits Your Template)

```python
def countUnivalTrees(root):
    
    count = 0

    def dfs(node):
        nonlocal count

        if node is None:
            return True

        left = dfs(node.left)
        right = dfs(node.right)

        if not left or not right:
            return False

        if node.left and node.left.data != node.data:
            return False

        if node.right and node.right.data != node.data:
            return False

        count += 1
        return True

    dfs(root)
    return count
```

---

## 🧪 Example (Sample Input 2)

Tree:

```
        1
      /   \
     2     3
    /     / \
   2     3   4
        / \
       3   3
```

✅ Unival subtrees:

- All leaf nodes
    
- Subtree rooted at value 3 with two children 3
    

Total = **6**

---

## 📊 Comparison Table

|Approach|Time|Space|Use|
|---|---|---|---|
|Brute Force|O(N²)|O(H)|❌ Avoid|
|Better|O(N)|O(H)|⚠️ OK|
|Optimal|O(N)|O(H)|✅ BEST|

---

## 🧠 Memory Trick (Interview Gold)

> **Tree + condition + subtree info → Post-order recursion**

---

## 🚀 Want More?

I can:

- Dry-run recursion step by step
    
- Convert to **C++ / Java**
    
- Explain how interviewers expect the answer
    
- Give similar tree problems for practice
    

Just tell me 😊

# You are given two binary search trees of integers having **_‘N’_** and **_‘M’_** nodes. Return an array that contains elements of both BST in sorted order.  A binary search tree (BST) is a binary tree data structure with the following properties.

```
• The left subtree of a node contains only nodes with data less than the node’s data.

• The right subtree of a node contains only nodes with data greater than the node’s data.

• Both the left and right subtrees must also be binary search trees.
```
##### Sample Input 1:

```
2 1 3 -1 -1 -1 -1
4 -1 -1
```

##### Sample Output 1:

```
1 2 3 4 
```

##### Explanation For Sample Output 1:

```
 The given BST are:-
```
![[Pasted image 20260207192829.png]]
![[Pasted image 20260207192840.png]]
```
The output will be 1 2 3 4
```

##### Sample Input 2:

```
4 2 7 -1 3 -1 -1 -1 -1  
5 1 7 -1 -1 -1 -1
```

##### Sample Output 2:

```
1 2 3 4 5 7 7 
```

##### Constraints:

```
1 <= 'N', 'M' <= 10^5

Time Limit: 1 sec
```

Nice work 👏👏  
You **debugged it correctly**, understood the platform expectation, and now you have an **accepted solution**. That’s solid learning right there.

Now let me give you **clean, exam-ready answers** for **Brute Force, Better, and Optimal** solutions — exactly how you can write/explain them in tests or interviews.

---

# ✅ Problem Recap (in simple words)

You are given **two Binary Search Trees (BSTs)**.  
You must **merge them and return a BST** that contains **all elements in sorted order**.

Key rule:

> Inorder traversal of a BST gives elements in sorted order.

---

# 1️⃣ Brute Force Solution

### 💡 Idea

1. Traverse **both BSTs**
    
2. Store all elements in one array
    
3. **Sort the array**
    
4. Convert sorted array into a **BST**
    
5. Return the BST root
    

---

### 🔧 Steps

- Do inorder traversal of BST1 → array
    
- Do inorder traversal of BST2 → array
    
- Sort array
    
- Build BST from sorted array
    

---

### 🧠 Code (Brute Force)

```python
def inorder(root, arr):
    if not root:
        return
    inorder(root.left, arr)
    arr.append(root.data)
    inorder(root.right, arr)


def sortedArrayToBST(arr):
    if not arr:
        return None
    mid = len(arr) // 2
    root = TreeNode(arr[mid])
    root.left = sortedArrayToBST(arr[:mid])
    root.right = sortedArrayToBST(arr[mid + 1:])
    return root


def mergeBST(root1, root2):
    arr = []
    inorder(root1, arr)
    inorder(root2, arr)

    arr.sort()
    return sortedArrayToBST(arr)
```

---

### ⏱ Complexity

- Time: **O((N + M) log(N + M))**
    
- Space: **O(N + M)**
    

### ✅ Pros / ❌ Cons

✔ Very easy  
❌ Sorting makes it slow

---

# 2️⃣ Better Solution

### 💡 Idea

1. Inorder traversal of BST1 → sorted list A
    
2. Inorder traversal of BST2 → sorted list B
    
3. Merge two sorted arrays
    
4. Convert merged array into BST
    

---

### 🔧 Steps

- Get two sorted arrays
    
- Merge like merge sort
    
- Build BST
    

---

### 🧠 Code (Better)

```python
def inorder(root, arr):
    if not root:
        return
    inorder(root.left, arr)
    arr.append(root.data)
    inorder(root.right, arr)


def mergeArrays(a, b):
    i = j = 0
    res = []

    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            res.append(a[i])
            i += 1
        else:
            res.append(b[j])
            j += 1

    res.extend(a[i:])
    res.extend(b[j:])
    return res


def sortedArrayToBST(arr):
    if not arr:
        return None
    mid = len(arr) // 2
    root = TreeNode(arr[mid])
    root.left = sortedArrayToBST(arr[:mid])
    root.right = sortedArrayToBST(arr[mid + 1:])
    return root


def mergeBST(root1, root2):
    a, b = [], []
    inorder(root1, a)
    inorder(root2, b)

    merged = mergeArrays(a, b)
    return sortedArrayToBST(merged)
```

---

### ⏱ Complexity

- Time: **O(N + M)**
    
- Space: **O(N + M)**
    

### ✅ Why better?

✔ No sorting  
✔ Linear time  
❌ Still uses extra arrays

---

# 3️⃣ Optimal Solution (Your Accepted One 🔥)

### 💡 Idea

- Use **two stacks**
    
- Do **simultaneous inorder traversal**
    
- Merge elements **on the fly**
    
- Build BST from final sorted list
    

---

### 🧠 Code (Optimal – Accepted)

```python
def sortedArrayToBST(arr):
    if not arr:
        return None

    mid = len(arr) // 2
    root = TreeNode(arr[mid])
    root.left = sortedArrayToBST(arr[:mid])
    root.right = sortedArrayToBST(arr[mid + 1:])
    return root


def mergeBST(root1, root2):
    stack1, stack2 = [], []
    result = []

    while root1 or root2 or stack1 or stack2:

        while root1:
            stack1.append(root1)
            root1 = root1.left

        while root2:
            stack2.append(root2)
            root2 = root2.left

        if not stack2 or (stack1 and stack1[-1].data <= stack2[-1].data):
            node = stack1.pop()
            result.append(node.data)
            root1 = node.right
        else:
            node = stack2.pop()
            result.append(node.data)
            root2 = node.right

    return sortedArrayToBST(result)
```

---

### ⏱ Complexity

- Time: **O(N + M)**
    
- Space: **O(H1 + H2 + N + M)**  
    (stacks + result array)
    

✔ Fast  
✔ Interview-grade  
✔ Platform-accepted

---

## 📊 Final Comparison

|Approach|Time|Space|Level|
|---|---|---|---|
|Brute Force|O((N+M)log(N+M))|O(N+M)|Beginner|
|Better|O(N+M)|O(N+M)|Intermediate|
|Optimal|O(N+M)|O(H1+H2)|Advanced|

---

## 🎯 How to explain in interview (1-liner)

> “I used inorder traversal to get sorted values from BSTs, merged them efficiently, and constructed a balanced BST from the merged result.”

---

If you want next:

- How to **optimize space further**
    
- How to answer this in **2 minutes verbally**
    
- Convert to **C++ / Java**
    
- Similar problems to practice
    

Just tell me 👍