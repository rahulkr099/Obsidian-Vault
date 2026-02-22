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
