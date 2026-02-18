# 1. You are given an array of integers 'ARR' of length 'N' and an integer Target. Your task is to return all pairs of elements such that they add up to Target.

Note:

```
We cannot use the element at a given index twice.
```

Follow Up:

```
Try to do this problem in O(N) time complexity. 
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 ≤ n ≤ 105
1 ≤ arr[i] ≤ 105

Where 'T' denotes the number of test cases, 'N' represents the size of the array, 'TARGET' represents the sum required, and 'ARR[i]' represents array elements.

Time Limit: 1 sec.
```

**Sample Input 1 :**

```
2 = two inputs
4 9  {4 is number of elements and 9 is target element}
2 7 11 13
5 1  {5 is number of elements and 1 is target element}
1 -1 -1 2 2
```

**Sample Output 1:**

```
2 7
-1 2
-1 2
```

**Explanation for Sample 1:**

```
For the first test case, we can see that the sum of 2 and 7 is equal to 9 and it is the only valid pair.

For the second test case, there are two valid pairs (-1,2) and (-1,2), which add up to 1.
```

**Sample Input 2 :**

```
1  = one input
4 16 {4 is number of elements and 16 is target element}
2 7 11 13
```

**Sample Output 2 :**

```
-1 -1
```

## Answer
## Brute Force Approach ( O (n^2) )
take an empty list
Run loops such that:
	current element + next element = target
	 append it to list
### Better Approach ( O(n log n) )
sort the array
take an empty list
take two pointer "left" and "right" pointer
		arr[left]  + arr[right]  == target
		append it to list

### Optimal Approach (Hashing)  O(n)
take an empty map of name "seen"
take an empty list of name "pairs"
1. Calculate the **needed number** by subtracting target and number
2. Check if we have **already seen** that number
3. If yes → we found a valid pair
4. Store the pair
5. Otherwise → remember the current number

We use a **hash map (dictionary)** to remember previously seen numbers.d 