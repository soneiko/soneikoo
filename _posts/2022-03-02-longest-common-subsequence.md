---
title: Longest Common Subsequence
---

```python
Difficulty: 'Hard'
Category:   'Dynamic Programming'
```

# Longest Common Subsequence
Write a function that takes in two strings and returns their longest common subsequence.

A subsequence of a string is a set of characters that aren't necessarily adjacent in the string but that are in the same order as they appear in the string. For instance, the characters `["a", "c", "d"]` form a subsequence of the string `"abcd"`, and so do the characters `["b", "d"]`. Note that a single character in a string and the string itlsef are both valid subsequences of the string.

You can assume that there will only be one longest common subsequence. 

**Sample Input**
```python
str1 = "ZXVVYZW"
str2 = "XKYKZPW"
```

**Sample Output**
```python
["X", "Y", "Z", "W"]
```

**Solution**

Longest Common Subsequence (LCS) is classical 2D dynamic programming problem. I solved it many times in my life, but every time it is equally hard to implement the solving idea. It requires precision and imagination. 

Declare 2D array called `dp = [][]`, where `dp[i][j]` is the length of the longest common subsequence of two prefixes: prefix of `str1` with length `i` and prefix of `str2` with length `j`. Having this, our dynamics transition will be:
```python
dp[i][j] = max(max(dp[i][j - 1], dp[i - 1][j]), dp[i - 1][j - 1] + 1)
```
And at the end, `dp[N][M]` where `N = length(str1); M = length(str2)` will be the correct answer. But it will be only the *length* of the LCS we wanted to find. But we need LCS itself.

Gladfully, we can restore the LCS letters. And this technique is just a beautiful masterpiece. Declare 2D array called `parent = [][]`, where `parent[i][j]` equals to triplet of values `(I, J, isTaken)`:
* `I` and `J` are the indexes in `dp` array from where we came to `dp[i][j]`. So, in other words `I` can be equal to either `i - 1` or to `i`. So does `J`, it can be equal either to `j - 1` or to `j`.
* `isTaken` is just a boolean value. If it is True, it means `str1[i]` or `str2[j]`(they are equal in this case) is taken (included) to LCS. If it is False, then neither `str1[i]` taken, nor `str2[j]`.

Having this 2D array `parent` we can restore the LCS itself. It can be done beutifully by tail recursion. Refer to the code below to see what I mean (function `traverseParent`).
```python
def traverseParent(i, j, parent, str1, ans):
    if i < 1 or j < 1:
        return
	
    if parent[i][j][2]:
        ans.append(str1[i])
	
    traverseParent(parent[i][j][0], parent[i][j][1], parent, str1, ans)

def longestCommonSubsequence(str1, str2):
    N, M = len(str1), len(str2)
    dp = [[0] * (M + 1) for i in range(N + 1)]
    parent = [[-1] * (M + 1) for i in range(N + 1)]
    str1, str2 = '*' + str1, '*' + str2
	
    for i in range(1, N + 1):
        for j in range(1, M + 1):
            if dp[i][j - 1] > dp[i - 1][j]:
                dp[i][j] = dp[i][j - 1]
                parent[i][j] = (i, j - 1, False,)
            else:
                dp[i][j] = dp[i - 1][j]
                parent[i][j] = (i - 1, j, False,)
			
            if str1[i] != str2[j]:
                continue
			
            increment = dp[i - 1][j - 1] + 1
			
            if increment > dp[i][j]:
                dp[i][j] = increment
                parent[i][j] = (i - 1, j - 1, True,)
	
    reversedAns = []
    traverseParent(N, M, parent, str1, reversedAns)
	
    return reversedAns[::-1]			
```
