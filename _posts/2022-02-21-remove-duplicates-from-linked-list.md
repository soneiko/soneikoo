---
title: Remove Duplicates From Linked List
---

```python
Difficulty: 'Easy'
Category:   'Linked Lists'
```

**Problem statement**

You're given the head of a Singly Linked List whose nodes are in sorted order with respect to their values. Write a function that returns a modified version of the Linked List that doesn't contain any nodes with duplicate values. The Linked List should be modified in place (i.e., you shouldn't create a brand new list), and the modified Linked List should still have its nodes sorted with respect to their values.

Each `LinkedList` node has an integer `value` as well as a `next` node pointing to the next node in the list or to `None` / `null` if it's the tail of the list. 

**Sample Input**
```python
linkedList = 1 -> 1 -> 3 -> 4 -> 4 -> 4 -> 5 -> 6 -> 6 # the head node with value 1
```

**Sample Output**
```python
1 -> 3 -> 4 -> 5 -> 6 # the head node with value 1
```

**Solution**

Solving idea is easy to come up with. So, we need to remove duplicates, but notice that these duplicates are located in consecutive subpart of the given Linked List. This is the main observation. Now, we need to get rid of that parts, in other words - compress them to one value. (i.e., instead of `4 -> 4 -> 4`, we need `4`). 

This is easy to do job with two inner loops. Outer loop for traversing the list, inner loop for traversing duplicate parts and collapsing them. Refer to the code below, if you are not familiar with this technique.
```python
class LinkedList:
    def __init__(self, value):
        self.value = value
        self.next = None


def removeDuplicatesFromLinkedList(linkedList):
    head = linkedList
	
    while head != None:
        curValue = head.value
        curNode = head.next
		
        while curNode != None:
            if curValue != curNode.value:
                break
				
            curNode = curNode.next
		
        head.next = curNode
        head = curNode
		
    return linkedList
```
