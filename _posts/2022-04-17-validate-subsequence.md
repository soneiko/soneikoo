---
title: Validate Subsequence
---

```python
Difficulty: 'Easy'
Category:   'Arrays'
```
# Validate Subsequence
Given two non-empty arrays of integers, write a function that determines whether the second array is a subsequence of the first one. 

A subsequence of an array is a set of numbers that aren't necessarily adjacent in the array but that are in the same order as they appear in the array. For instance, the numbers `[1, 3, 4]` form a subsequence of the array `[1, 2, 3, 4]`, and so do the numbers `[2, 4]`. Note that a single number in an array and the array itself are both valid subsequences of the array. 

**Sample Input**
```python
array = [5, 1, 22, 25, 6, -1, 8, 10]
sequence = [1, 6, -1, 10]
```

**Sample Output**
```python
True
```

**Solution**

Solution is Two Pointers technique. Create two pointers, first pointing to the array, second to the subsequence. In nested loops, move them to the right (or increase their values). Handle edge cases. That's it.

```python
def isValidSubsequence(array, sequence):
    pointer = 0
    pointer_arr = 0
	
    while pointer < len(sequence):
        if pointer_arr >= len(array):
            break
		
        while pointer_arr < len(array):
            if array[pointer_arr] == sequence[pointer]:
                pointer_arr += 1
                break
            pointer_arr += 1
		
        if array[pointer_arr - 1] == sequence[pointer]:
            pointer += 1
	
    return True if pointer >= len(sequence) else False
```
