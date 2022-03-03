---
title: Smallest Difference
---

```python
Difficulty: 'Medium'
Category:   'Arrays'
```
# Smallest Difference
Write a function that takes in two non-empty arrays of integers, finds the pair of numbers (one from each array) whose absolute difference is closest to zero, and returns an array containing these two numbers, with the number from the first array in the first position.

Note that the absolute difference of two integers is the distance between them on the real number line. For example, the absolute difference of -5 and 5 is 10, and the absolute difference of -5 and -4 is 1.

You can assume that there will only be one pair of numbers with the smallest difference.

**Sample Input**
```python
arrayOne = [-1, 5, 10, 20, 28, 3]
arrayTwo = [26, 134, 135, 15, 17]
```

**Sample Output**
```python
[28, 26]
```

**Solution**

I love *two pointer* problems. I just love them. It is just beautiful how this simple technique can reduce quadratic time complexity to linear one.

First, sort two input arrays in ascending order. Then declare two pointers, one will be pointing to the first array, another to the second array. Iterate until pointers are in valid range, and during iteration depending on comparison of values being pointed either move `pointerOne` to the right, or move `pointerTwo` to the right. And in every iteration - try to update the final answer. That's it!
```python
def smallestDifference(arrayOne, arrayTwo):
    arrayOne.sort()
    arrayTwo.sort()
	
    pointerOne, pointerTwo = 0, 0
    smallestDiff, ansPair = float('inf'), []
	
    while pointerOne < len(arrayOne) and pointerTwo < len(arrayTwo):
        if arrayOne[pointerOne] == arrayTwo[pointerTwo]:
            return [arrayOne[pointerOne]] * 2
		
        absDiff = abs(arrayOne[pointerOne] - arrayTwo[pointerTwo])
			
        if absDiff < smallestDiff:
            smallestDiff = absDiff
            ansPair = [arrayOne[pointerOne], arrayTwo[pointerTwo]]
		
        if arrayOne[pointerOne] < arrayTwo[pointerTwo]:
            pointerOne += 1
        else:
            pointerTwo += 1
	
    return ansPair
```
