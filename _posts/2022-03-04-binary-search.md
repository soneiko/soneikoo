---
title: Binary Search
---

```python
Difficulty: 'Easy'
Category:   'Searching'
```
# Binary Search
Write a function that takes in a sorted array of integers as well as a target integer. The function should use the Binary Search algorithm to determine if the target integer is contained in the array and should return its index if it is, otherwise `-1`.

**Sample Input**
```python
array = [0, 1, 21, 33, 45, 45, 61, 71, 72, 73]
target = 33
```

**Sample Output**
```python
3
```

**Solution**

If you are unfamiliar with Binary Search or have even not implemented it at least 10 times in your life, then you're visiting totally wrong site. Please, go do your CS fundamentals.
```python
def binarySearch(array, target):
    left, right = 0, len(array) - 1
	
    while left < right - 1:
        middle = (left + right) // 2
		
        left = middle if array[middle] < target else left
        right = middle if array[middle] >= target else right
	
    isLeft = array[left] == target
    isRight = array[right] == target
	
    if not isLeft and not isRight:
        return -1
		
    return left if isLeft else right
```
