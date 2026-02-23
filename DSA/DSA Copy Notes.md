# Array

## ✅ Python Program (Manual Insertion – Interview Style)

```python
def insert_element(arr, pos, value):
    n = len(arr)

    # Check for valid position
    if pos < 0 or pos > n:
        print("Invalid position")
        return arr

    # Increase array size by 1
    arr.append(0)

    # Shift elements to the right
    for i in range(n - 1, pos - 1, -1):
        arr[i + 1] = arr[i]

    # Insert new value
    arr[pos] = value

    return arr


# Driver code
arr = list(map(int, input("Enter elements: ").split()))
pos = int(input("Enter position: "))
value = int(input("Enter value: "))

arr = insert_element(arr, pos, value)

print("Updated array:", arr)
```

---
## 🧠 How to Explain in Interview (Simple Words)

You can say something like this:

👉 _"To insert an element at a specific position in an array, first we check if the position is valid. Then we increase the size of the array. After that, we shift all elements to the right from that position to make space. Finally, we place the new element at the required position."_

## ⏱ Time Complexity

- **O(n)** → because we may need to shift all elements
---

## ⚡ Bonus (What interviewer may ask next)

Be ready for these follow-ups:

1. **Built-in method?**
    ```python
    arr.insert(pos, value)
    ```
    
2. **Difference between array and list in Python?**
    
    - List = dynamic
        
    - Array (C) = fixed size
        
3. **Best case vs worst case**
    
    - Best: O(1) (insert at end)
        
    - Worst: O(n) (insert at beginning)
        

---
Nice 👍 this is another **classic interview question**. Let’s make your answer clean, simple, and confident.

---

## ✅ Python Program (Manual Deletion – Interview Style)

```python
def delete_element(arr, pos):
    n = len(arr)

    # Check for valid position
    if pos < 0 or pos >= n:
        print("Invalid position")
        return arr

    # Shift elements to the left
    for i in range(pos, n - 1):
        arr[i] = arr[i + 1]

    # Remove last duplicate element
    arr.pop()

    return arr


# Driver code
arr = list(map(int, input("Enter elements: ").split()))
pos = int(input("Enter position to delete: "))

arr = delete_element(arr, pos)

print("Updated array:", arr)
```

---

## 🧠 How to Explain in Interview

You can say:

👉 _"To delete an element from a specific position, first we check if the position is valid. Then we shift all elements to the left starting from that position to fill the gap. Finally, we remove the last element to maintain the correct size of the array."_

---

## ⏱ Time Complexity

- **O(n)** → because shifting is required
    

---

## ⚡ Bonus (Follow-up Questions)

### 1. Built-in Method

```python
arr.pop(pos)
```

---

### 2. Delete by Value

```python
arr.remove(value)
```

---

### 3. Best vs Worst Case

- Best: O(1) → delete last element
    
- Worst: O(n) → delete from beginning
    

---

Great 👍 this is a **very important linked list question** — often asked in interviews.

Let’s keep it simple and clear so you can explain confidently.

---
# Linked List
## ✅ Python Program (Insertion at Beginning in Linked List)

```python
# Node class
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


# Function to insert at beginning
def insert_at_beginning(head, value):
    new_node = Node(value)   # create new node
    new_node.next = head     # point new node to current head
    head = new_node          # update head
    return head


# Function to print linked list
def print_list(head):
    temp = head
    while temp:
        print(temp.data, end=" -> ")
        temp = temp.next
    print("None")


# Driver code
head = None

# Creating list
n = int(input("Enter number of elements: "))
for _ in range(n):
    value = int(input("Enter value: "))
    head = insert_at_beginning(head, value)

print("Linked List:")
print_list(head)
```

---

## 🧠 How to Explain in Interview

You can say:

👉 _"To insert at the beginning of a linked list, we first create a new node. Then we make its next pointer point to the current head. After that, we update the head to this new node."_

---

## ⏱ Time Complexity

- **O(1)** ✅ (Very important point)
    

👉 No traversal needed — constant time operation

---

## 🔥 Why This is Important

Interviewers like this because:

- Tests pointer understanding
    
- Foundation for stacks & advanced structures
    

---

## ⚡ Follow-up Questions

Be ready for these:

### 1. Why is it O(1)?

👉 No loop, just pointer change

### 2. What if list is empty?

👉 Head is `None`, still works perfectly

### 3. Insert at end vs beginning?

- Beginning → O(1)
    
- End → O(n) (if no tail pointer)
    

---

## 🚀 Pro Tip

If you say this line in interview, it’s powerful:

👉 _"Insertion at beginning is preferred when we need constant time operations, like in stack implementation using linked list."_

---

If you want next level 🚀  
I can give:

- Insertion at end
    
- Insertion at position
    
- Doubly linked list version
    
- Real interview problems
    

Just tell me 👍