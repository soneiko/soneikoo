---
title: Bubble Sort
---

```python
Difficulty: 'Easy'
Category:   'Sorting'
```

# Bubble Sort
Write a function that takes in an array of integers and returns a sorted version of that array. Use the Bubble Sort algorithm to sort the array.


**Sample Input**
```python
array = [8, 5, 2, 9, 5, 6, 3]
```

**Sample Output**
```python
[2, 3, 5, 5, 6, 8, 9]
```

**Solution**

Bubble sort is based on swapping neighboring elements. In worst case (maximum), N (length of input array) iterations needed. In each iteration, swap all neighboring elements which do not satisfy the needed order. 

```python
def bubbleSort(array):
    SIZE = len(array)
	
    for n in range(SIZE):
        for i in range(SIZE - 1):
            if array[i] > array[i + 1]:
                array[i], array[i + 1] = array[i + 1], array[i]
	
    return array
```
