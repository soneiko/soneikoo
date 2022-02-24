---
title: Nth Fibonacci
---

```python
Difficulty: 'Easy'
Category:   'Recursion'
```
# Nth Fibonacci
The Fibonacci sequence is defined as follows: the first number of the sequence is `0`, the second number is `1`, and the nth number is the sum of the (n - 1)th and (n - 2)th numbers. Write a function that takes in an integer `n` and returns the nth Fibonacci number. 

Important note: the Fibonacci sequence is often defined with its first two numbers as `F0 = 0` and `F1 = 1`. For the purpose of this question, the first Fibonacci number is `F0`; therefore, `getNthFib(1)` is equal to `F0`, `getNthFib(2)` is equal to `F1`, etc..

**Sample Input #1**
```python
n = 2
```

**Sample Ouput #1**
```python
1 # 0, 1
```

**Sample Input #2**
```python
n = 6
```

**Sample Output #2**
```python
5 # 0, 1, 1, 2, 3, 5
```

**Solution**

This is the most basic and classic problem for Recursion. Solution code of it shows the beaty of recursion and how amazing things could happen with several lines of code. 

Below, you can find three different solutions. Each of them deserves to be written even if some are not optimal. Let's compare them:
1. The most beautiful solution. But time complexity `O(2 ^ n)`, space complexity `O(n)` (because of recursion stack).
2. Solution which shows the power of memoization technique and how it can reduce complexity from exponential to linear. Time complexity `O(n)`, space `O(n)`.
3. This is optimal solution, although it's not recursive. `O(n)` time, `O(1)` space.


```python
def getNthFib(n):
    if n <= 1:
        return 0
	
    if n == 2:
        return 1
	
    return getNthFib(n - 1) + getNthFib(n - 2)
```
```python
def getNthFib(n, memo={1:0, 2:1}):
    if n in memo:
        return memo[n]
	
    memo[n] = getNthFib(n - 1, memo) + getNthFib(n - 2, memo)
	
    return memo[n]
```
```python
def getNthFib(n):
    lastTwo = [0, 1]
	
    curN = 3
    while curN <= n:
        Nth = lastTwo[0] + lastTwo[1]
        lastTwo[0] = lastTwo[1]
        lastTwo[1] = Nth
		
        curN += 1
	
    return lastTwo[1] if n > 1 else 0
```
