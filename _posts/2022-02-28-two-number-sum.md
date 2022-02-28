---
title: Two Number Sum
---

```python
Difficulty: 'Easy'
Category:   'Arrays'
```

# Two Number Sum

Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. If any two numbers in the input array sum up to the target sum, the function should return them in an array, in any order. If no two numbers sum up to the target sum, the function should return an empty array.

Note that the target sum has to be obtained by summing two different integers in the array; you can't add a single integer to itself in order to obtain the target sum.

You can assume that there will be at most one pair of numbers summing up to the target sum. 

**Sample Input**
```python
array = [3, 5, -4, 8, 11, 1, -1, 6]
targetSum = 10
```

**Sample Output**
```python
[-1, 11] # the numbers could be in reverse order
```

**Solution**

I started problem-solving in 8th grade at school. At that time, I could solve this problem, but in `O(n ^ 2)` time. Obviously, now I can in `O(n)`.

I want to answer one popular question I have been asked a lot: 'Is knowledge of math necessary to study algorithms?'
> Knowing math is a sufficient condition, but not necessary. Because math is much more complicated than algorithms.


```python
def twoNumberSum(array, targetSum):
    appeared = dict()
	
    for number in array:
        if targetSum - number in appeared:
            return [number, targetSum - number]
        appeared[number] = True
	
    return []
```
