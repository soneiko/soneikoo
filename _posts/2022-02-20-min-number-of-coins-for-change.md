---
title: Min Number Of Coins For Change
---

```python
Difficulty: 'Medium'
Category:   'Dynamic Programming'
```
# Min Number Of Coins For Change
Given an array of positive integers representing coin denominations and a single non-negative integer `n` representing a target amount of money, write a function that returns the smallest number of coins needed to make change for (to sum up to) that target amount using the given coin denominations.

Note that you have access to an unlimited amount of coins. In other words, if the denominations are `[1, 5, 10]`, you have access to an unlimited amount of `1`s, `5`s, and `10`s.

If it's impossible to make change for the target amount, return `-1`.

**Sample Input**
```python
n = 7
denoms = [1, 5, 10]
```

**Sample Output**
```python
3  # 2x1 + 1x5
```

**Solution**

As problem tags say it is medium dynamic programming problem. After reading the problem carefully, it is obvious that this is one-dimensional dynamic programming. In one-dimensional DP we traditionally have one-dimensional array with answers, let's call our array `memo = []`. 

Let `memo[i]` be the smallest number of coins needed to make change for amout `i`. In other words, `memo[i]` is the answer for `i`. 
Okay, imagine that our future algorithm is working and currently trying to calculate the answer for `memo[i]`, meanwhile assume that we already have correct answers for every `j`, such that `0 < j < i`, it means we have `memo[1], memo[2], ..., memo[i - 1]`. Okay, having this and also without limitation of generality assume that our coin denominations are `[1, 5, 10]`. So, what do you think `memo[i]` will be equal to? Yeah, of course it is `memo[i] = min(memo[i - 1], memo[i - 5], memo[i - 10]) + 1` .
Okay, we have our so called DP transition rule. What about DP base? It is of course `memo[0] = 0`.

```python
def minNumberOfCoinsForChange(n, denoms):
    memo = [None for _ in range(n + 1)]
    memo[0] = 0
		
    ans = helper(n, denoms, memo)
		
    return ans if ans != float("inf") else -1


def helper(n, denoms, memo):
    if n < 0:
        return float("inf")
				
    if memo[n] != None:
        return memo[n]
	
    minAmount = float("inf")
	
    for denom in denoms:
        minAmount = min(minAmount, helper(n - denom, denoms, memo))
	
    memo[n] = minAmount + 1
	
    return memo[n]
```
