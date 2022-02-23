---
title: Rectangle Mania
layout: default
---

```python
Difficulty: 'Very Hard'
Category:   'Graphs'
```
# Rectangle Mania
Write a function that takes in a list of Cartesian coordinates (i.e., (x, y) coordinates) and returns the number of rectangles formed by these coordinates.

A rectangle must have its four corners amongst the coordinates in order to be counted, and we only care about rectangles with sides parallel to the x and y axes (i.e., with horizontal and vertical sides -- no diagonal sides).

You can also assume that no coordinate will be farther than 100 units from the origin.

**Sample Input**
```python
coords = [
    [0, 0], [0, 1], [1, 1], [1, 0],
    [2, 1], [2, 0], [3, 1], [3, 0],
]
```

**Sample Output**
```python
6
```

**Solution**

At first I was afraid from this problem. Because I saw its diffculty level - Very hard, than its category - Graphs. And also I am traditionally bad in Geometry problems. Very bad. But then, I started to decompose the problem.

Think of a 4 points which form a needed rectangle. Keep in mind that sides are perpendicular to axes and points are integers. Then, go even more simpler. Throw away two horizontal edges of a rectangle and keep only two side vertical edges. One vertical edge is formed from two points which have same x-coordinate and different y-coordinate. Then, forget about that rectangles, think only about this vertical edges. Imagine a lot of vertical edges in 2D coordinate system. Which two of them form a rectangle? Ones that are in the same level. Ones that have different levels do not form a rectangle. 

Okay, these observations led me to the very first key idea which helped me to solve the problem. Idea is, think that given set of points form a gate. Common black coloured gate which we have a lot in Tashkent in front of official buildings. Why is this important? Because I can represent this gate very easily in Python, as dictionary of arrays. And also, I can iterate it, and somehow try to calculate something. 

Okay, let’s say we are iterating through this gate from left to right and currently we are at some vertical line of that gate and fixed some vertical edge in that line. So, we have one vertical edge in our hand. How many rectangles could be formed from that one vertical edge, so that this edge is a left side of a rectangle? It is easy to calculate, just open inner loop and iterate to the right side from that line and check if the new line has two points with the same height as in our edge. So, what do we have? For one fixed vertical edge we can easily find the answer. This means if we somehow can iterate through all that vertical edges, than we can find the final answer. But there is one little problem. It is simple, if line of a gate has 2 points. 2 points form only one edge. But what if it has let’s say 10 points. How many vertical edges can be formed from 10 points? Answer is 45. And it is a little problematic to iterate through all this 45 edges. What if there are not 10, but 100 points in one line? 

Now, here I came up with second key idea. And idea is, let’s not fix the vertical edge. Instead fix one vertical line of the gate. And take another vertical line. Intersect them, so that only points with equal height remains. Let’s say there left N points in one line and N points in another line. 2*N points. How many rectangles can be formed from them? It is N * (N - 1) / 2. 

Thank you for your attention. I want to dedicate this solution to my mom. She is the best person in the world.

```python
def rectangleMania(coords):
    coords_dict = dict()
	
    for coord in coords:
        x_coord, y_coord = coord
		
        if x_coord not in coords_dict:
            coords_dict[x_coord] = [y_coord]
        else:
            coords_dict[x_coord].append(y_coord)
			
    ans = 0
	
    for x_iter in range(-100, 101, 1):
        if x_iter not in coords_dict:
            continue
        for x2_iter in range(x_iter + 1, 101, 1):
            if x2_iter not in coords_dict:
                continue
            n = len(set(coords_dict[x_iter]) & set(coords_dict[x2_iter]))
            ans += n * (n - 1) // 2
	
    return ans
```
