---
title: Validate BST
---

```python
Difficulty: 'Medium'
Category:   'Binary Search Trees'
```
# Validate BST
Write a function that takes in a potentially invalid Binary Search Tree (BST) and returns a boolean representing whether the BST is valid.

Each `BST` node has an integer `value`, a `left` child node, and a `right` child node. A node is said to be a valid `BST` node if and only if it satisfies the BST property: its `value` is strictly greater than the values of every node to its left; its `value` is less than or equal to the values of every node to its right; and its children nodes are either valid `BST` nodes themselves or `None`/`null`.

A BST is valid if and only if all of its nodes are valid `BST` nodes.

**Sample Input**
```python
tree =         10
              /  \
	     5    15
	   /  \  /  \
          2   5 13   22
         /        \
	1          14
```

**Sample Output**
```python
True
```

**Solution**

This is very a fundamental problem of Binary Search Trees. I can paraphrase the big problem statement above with one sentence: Check, whether given binary tree is binary search tree or not. This is what asked from us.

Actually, solution is not ordinary and very elegant. Because it uses recursion in a non-conventional way. First, it shows the full power of input parameters of a recursive function. Second, it shows a top-down approach of recursion. Because, traditionally for our brains it is easier to imagine bottom-up approach of a recursion.

So, all we do is - maintain two limit parameters. Left limit and Right limit. And check if current node's value located inside this interval. Tricky and beautiful part is - updating these limits.  Check the code below, to see what I mean.
```python
class BST:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def validateBst(tree, leftLimit=float('-inf'), rightLimit=float('inf')):
    if not tree:
        return True
	
    if not leftLimit <= tree.value <= rightLimit:
        return False
	
    isLeftBst = validateBst(tree.left, leftLimit, tree.value - 1)
    isRightBst = validateBst(tree.right, tree.value, rightLimit)
	
    return isLeftBst and isRightBst
```
