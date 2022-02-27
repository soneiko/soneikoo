---
title: Palindrome Check
---

```python
Difficulty: 'Easy'
Category:   'Strings'
```
# Palindrome Check
Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.

A palindrome is defined as a string that's written the same forward and backward. Note that single-character strings are palindromes.

**Sample Input**
```python
string = "abcdcba"
```

**Sample Output**
```python
True # it's written the same forward and backward
```

**Solution**

Although, this is very easy problem, in general, palindrome problems may become true nightmare. Especially, palinfrome + dynamic programming kind of problems. But ok, lets focus on this one.

I'll tell you right away, optimal time complexity is `O(n)`, optimal space complexity is `O(1)`. So, we should check palindromeness property in-place (not creating auxiliary string). Now, look at the sequence of paired integers below, what do you think they mean?:
* `0` <> `n - 1`
* `1` <> `n - 2`
* `2` <> `n - 3`
* .......................
* `n // 2 - 1` <> `(n + 1) // 2`


```python
def isPalindrome(string):
    i, length = 0, len(string)
    mid = length // 2
	
    while i < mid:
        if string[i] != string[length - i - 1]:
            return False
        i += 1
	
    return True
```
