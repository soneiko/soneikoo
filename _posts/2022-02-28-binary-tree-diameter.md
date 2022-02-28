---
title: Binary Tree Diameter
---

```python
Difficulty: 'Medium'
Category:   'Binary Trees'
```

# Binary Tree Diameter

Write a function that takes in a Binary Tree and returns its diameter. The diameter of a binary tree is defined as the length of its longest path, even if that path doesn't pass through the root of the tree. 

A path is a collection of connected nodes in a tree, where no node is connected to more than two other nodes. The length of a path is the number of edges between the path's first node and its last node.

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be `BinaryTree` nodes themselves or `None`/`null`.

**Sample Input**
```python
tree =           1
               /  \	
              3    2
            /  \
           7    4
          /      \
         8        5
        /          \
       9            6
```

**Sample Output**
```python
6 # 9 -> 8 -> 7 -> 3 -> 4 -> 5 -> 6
# There are 6 edges between the
# first node and the last node
# of this tree's longest path. 
```

**Solution**

The description says - medium problem, okay. The tricky part is that the diameter path does not have to pass from the root. 

Obviously, the solution is some modification of DFS. Let's say, our DFS  is currently processing some node. What will be the answer for this node, if we have correct answers from the left subtree and right subtree? Surely, it will be the maximum of those two. But what if diameter passes from the current node which we are processing now? Then, the answer will be the maximum of the length of the longest `path` from the left subtree and the length of the longest `path` from the right subtree. By longest `path`, I mean the path starting from the root of that subtree and ending at some of the leaves of that subtree.

So, this means our recursive function should be able to update and return 2 values: answer of its subtree and the length of the longest path of its subtree. 
```python
class BinaryTree:
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

def binaryTreeDiameter(tree):
    ans, _ = _binaryTreeDiameter(tree)
    return ans
		
def _binaryTreeDiameter(tree):
    if not tree:
        return 0, -1
	
    leftAns, leftLongestPath = _binaryTreeDiameter(tree.left)
    rightAns, rightLongestPath = _binaryTreeDiameter(tree.right)
	
    ans = max(max(leftAns, rightAns), leftLongestPath + rightLongestPath + 2)
    longestPath = max(leftLongestPath, rightLongestPath) + 1
	
    return ans, longestPath
```
