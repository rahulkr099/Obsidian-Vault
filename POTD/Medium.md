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

### ❓ Why do conflicts happen?

Because **two characters can have same frequency**.

We must **reduce frequencies** by deleting characters.

---

# 🔹 Detailed Code (No Shortcuts)

`def minDeletionsToUniqueFrequencies(s):     # STEP 1: Count frequency manually (like Counter)     freq = {}      for ch in s:         if ch in freq:             freq[ch] += 1         else:             freq[ch] = 1`

Now:

`s = "babccbc" freq = {'b': 3, 'a': 1, 'c': 3}`

---

### STEP 2: Track used frequencies

    `used_frequencies = set()     deletions = 0`

Why set?

- Fast lookup
    
- To ensure **no duplicate frequencies**
    

---

### STEP 3: Fix duplicate frequencies

    `for ch in freq:         count = freq[ch]`

Now check:

- If `count` already exists in `used_frequencies`
    
- Reduce it until unique
    

`while count > 0 and count in used_frequencies:             count -= 1      # delete one character             deletions += 1  # count deletion

Finally, store the unique frequency:


```if count > 0:             used_frequencies.add(count)`

---

### STEP 4: Return answer


```return deletions```