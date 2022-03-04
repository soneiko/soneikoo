---
title: Node Depths
---

```python
Difficulty: 'Easy'
Category:   'Binary Trees'
```
# Node Depths
The distance between a node in a Binary Tree and the tree's root is called the node's depth. 

Write a function that takes in a Binary Tree and returns the sum of its nodes' depths. 

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be `BinaryTree` nodes themselves or `None`/`null`.

**Sample Input**
```python
tree =         1
             /   \
	    2     3
           / \   / \
	  4   5 6   7
         / \
        8   9
 ```
 
 **Sample Output**
 ```python
 16
 # The depth of the node with value 2 is 1.  
 # The depth of the node with value 3 is 1.
 # The depth of the node with value 4 is 2.
 # The depth of the node with value 5 is 2.
 # Etc..
 # Summing all of these depths yields 16.
 ```
 
 **Solution**
 
 I don't know exactly, what technique is used in solution. Because it has inspiring ideas from such theories like Recursion, DFS, Divide&Conquer and Dynamic Programming. Beautilly, solution itself is very concise. Just look at the code, it doesn't require additional explanation. 
 ```python
def nodeDepths(root, depth=0):
    if not root:
        return 0
	
    leftSum = nodeDepths(root.left, depth + 1) 
    rightSum = nodeDepths(root.right, depth + 1) 
	
    return leftSum + rightSum + depth


class BinaryTree:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
 ```
