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

**My solution**: Although problem is labeled with *easy* mark, it is not that simple to implement the solving idea. Because expected answer is not just an integer value, but whole list with branch sums. Okay, yeah it's pretty easy to see that some modification of standard DFS algorithm is required here, since we were asked to order those branch sums from leftmost to rightmost. Only thing required additionally is to keep track of answer list which should ideally be declared in out scope of recursive DFS function. Other things are straightforward, everytime DFS hits the leaf, we add new answer to the answer list. Since, DFS traverses from left to right, the final answer will be ordered as expected. One important thing to remember is that in Python, standard list is reference-based variable. This means our list variable keeps only reference to its list, not the value itself. And the good thing about it for our solution is that, when everytime out recursive function is called passing this answer list variable: *first* - it is not going to be slow , *second* - when inner recursive call returns to outer recursive call, the possibly added answer value to that list will not be lost. 

But my solution is little bit more elegant than above. I am not declaring the answer list in outer scope, instead my recursive function returns list. Let's say, currently our DFS is at some node of the binary tree. And inner DFS call with left child returned answer list of left subtree, respectively inner DFS call with right child returned answer list of right subtree. And assuming that both answers are correct, only thing we need to do is combining the answers. But combining is also easy, we just need to append right answer to left one, since it would keep the order correctly. Honestly saying, this is more of a Divide&Conquer style solution rather than simple DFS modification.  

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
