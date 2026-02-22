# Array

### Insertion
Great 👍 this is a very common **interview question**, so I’ll give you a clean + explainable answer you can say confidently.

---

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
