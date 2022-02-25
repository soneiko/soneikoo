---
title: Balanced Brackets
---

```python
Difficulty: 'Medium'
Category:   'Stacks'
```
# Balanced Brackets
Write a function that takes in a string made up of brackets (`(`, `[`, `{`, `)`, `]`, `}`) and other optional characters. The function should return a boolean representing whether the string is balanced with regards to brackets.

A string said to be balanced if it has as many opening brackets of a certain type as it has closing brackets of that type and if no bracket is unmatched. Note that an opening bracket can't match a corresponding closing bracket that comes before it, and similarly, a closing bracket can't match a corresponding opening bracket that comes after it. Also, brackets can't overlap each other as in `[(])`.

**Sample Input**
```python
string = "([])(){}(())()()"
```

**Sample Output**
```python
True # it's balanced
```

**Solution**

Balanced Brackets is the most classic problem of Stacks. It truly shows how such simple principle as LIFO (last in - first out) can be so powerful. Solving idea is quite simple if you are familiar with it, otherwise it is tricky to come up with.

So, all we do is - maintain one stack for opening brackets of all type. While iterating given string from left to right:
1. If you see opening bracket, add it to the stack.
2. If you see closing bracket:<br>
    2.1. If stack is empty - return False. It means we found unmatched closing bracket. Unmatched because it              comes before its opening pair.<br>
    2.2. If closing bracket matches to top of the stack - pop the stack. Continue.<br>
    2.3. Else if closing bracket doesn't match top of the stack - return False. It means we found overlaping                      brackets.
3. If you see other character - just ignore it.

Finally, return True if stack is empty. If it is not, that means there were more opening brackets than closing ones.  
```python
def balancedBrackets(string):
    stack = []
    match = {')': '(', ']': '[', '}': '{'}
	
    for bracket in string:
        if bracket in ['(', '[', '{']:
            stack.append(bracket)
        elif bracket in match:
            if not stack:
                return False
			
            if match[bracket] == stack[-1]:
                stack.pop()
            else:
                return False
	
    return not stack
```
