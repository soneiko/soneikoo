---
title: Branch Sums
layout: default
---

**Difficulty**: Easy

**Category**: Binary Trees

**Problem statement**: Write a function that takes in a Binary Tree and returns a list of its branch sums ordered from leftmost branch sum to rightmost branch sum.

A branch sum is the sum of all values in a Binary Tree branch. A Binary Tree branch is a path of nodes in a tree that starts at the root node and ends at any leaf node.

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right`  child node. Children nodes can either be `BinaryTree` nodes themselves or `None` / `null`.

**Sample Input**:  
............................................................................<br>
`tree` = .........................1................................... <br>
................................../.........\\.............................. <br>
..............................2..............3........................... <br>
.........................../......\\......../......\\....................... <br>
........................4.........5.....6.........7.................... <br>
....................../....\\...../......................................... <br>
....................8......9..10....................................... <br>
............................................................................<br>

**Sample Output**:<br>
............................................................................<br>
.....\[15, 16, 18, 10, 11\]......................................<br>
.....\# 15 == 1 + 2 + 4 + 8...................................<br>
.....\# 16 == 1 + 2 + 4 + 9...................................<br>
.....\# 18 == 1 + 2 + 5 + 10.................................<br>
.....\# 10 == 1 + 3 + 6..........................................<br>
.....\# 11 == 1 + 3 + 7..........................................<br>
............................................................................<br>

**My solution**: something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something something 

**Code**:<br>
```python
class BinaryTree:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def branchSums(root, curSum=0):
    if root is None:
        return []
	
    if root.left is None and root.right is None:
        return [curSum + root.value]
	
    left_ans = branchSums(root.left, curSum + root.value)
    right_ans = branchSums(root.right, curSum + root.value)
	
    return left_ans + right_ans
```
