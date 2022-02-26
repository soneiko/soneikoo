---
title: Merge Overlapping Intervals
---

```python
Difficulty: 'Medium'
Category:   'Arrays'
```
# Merge Overlapping Intervals
Write a function that takes in a non-empty array of arbitrary intervals, merges any overlapping intervals, and returns the new intervals in no particular order.

Each `interval` is an array of two integers, with `interval[0]` as the start of the interval and `interval[1]` as the end of the interval.

Note that back-to-back intervals aren't considered to be overlapping. For example, `[1, 5]` and `[6, 7]` aren't overlapping; however, `[1, 6]` and `[6, 7]` *are* indeed overlapping.

Also note that the start of any particular interval will always be less than or equal to the end of the interval.

**Sample Input**
```python
intervals = [[1, 2], [3, 5], [4, 7], [6, 8], [9, 10]]
```

**Sample Output**
```python
[[1, 2], [3, 8], [9, 10]]
# Merge the intervals [3, 5], [4, 7], [6, 8].
# The intervals could be ordered differently.
```

**Solution**

Overlapping intervals is very popular problem. Despite its category being Arrays, I personally think the problem is about geometrical thinking. 

First thing you should figure out is that it cannot be solved in linear time, because not sorted intervals are given as input. That is why we need to sort them anyway, Sort them with respect to the start value of intervals.

Then, while iterating the sorted array from left to right:
1. If current interval overlaps with the last one in answer list - merge them and update the answer.
2. If current interval does not overlap - simply append it to anwer list.


```python
def mergeOverlappingIntervals(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for interval in intervals[1:]:
        if merged[-1][0] <= interval[0] <= merged[-1][1]:
            newMergedInterval = [merged[-1][0], max(merged[-1][1], interval[1])] 
            merged[-1] = newMergedInterval
        else:
            merged.append(interval)
    
    return merged
```
