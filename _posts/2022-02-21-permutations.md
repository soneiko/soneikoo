---
title: Permutations
---

```python
Difficulty: 'Medium'
Category:   'Recursion'
```

**Problem statement**

Write a function that takes in an array of unique integers and returns an array of all permutations of those integers in no particular order.

If the input array is empty, the function should return an empty array.

**Sample Input**
```python
array = [1, 2, 3]
```

**Sample Output**
```python
[[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]
```

**Solution**

This is the classic problem in problem-solving. It truly tests you understanding of recursion. And you should know that recursive functions can also work with outer-scope declared variables, not just with local ones. Especially `lists`, with them you can pass (save) data from inner recursive calls to outer ones. 

I recommend to analyze the code below. And I will also explain the solution looking to this code, because it is the best way in the case of this problem. So, function `_getPermutations` does all job. It is recursive function and its input parameters are 4 variables - all of them are lists:
1. `nums` - given array with unique integers
2. `used` - for every integer from nums list, we maintain one boolean used variable. If `used[i]` is True, it means that integer in position `i` (i.e., `nums[i]`) is used. Is used in current permutation which we are building. Yes, this function builds every single permutation one by one. This is actually elegant way of simple brute-forcing.
3. `curPerm` - some prefix of the permutation we are building. If its length equals to length of `nums`, this means we have built some correct permutation and can add it to the `ans`.
4. `ans` - our answer list. It contains all the permutations we have built. 

Now, just read the code and you should understand other things. If you didn't, then I am powerless. 
```python
def getPermutations(array):
    if len(array) == 0:
        return []
	
    ans, used, curPerm = [], {num : False for num in array}, []
    _getPermutations(array, used, curPerm, ans)
	
    return ans


def _getPermutations(nums, used, curPerm, ans):
    if len(curPerm) == len(nums):
        ans.append(curPerm.copy())
        return
	
    for num in nums:
        if not used[num]:
            curPerm.append(num)
            used[num] = True
            _getPermutations(nums, used, curPerm, ans)
            curPerm.pop()
            used[num] = False
```
