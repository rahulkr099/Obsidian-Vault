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

