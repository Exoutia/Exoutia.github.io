---
title: "K Closest Points to Origin"
date: 2023-12-25T18:25:21+05:30
author: "Bibek Jha"
image: /images/blogs/post3/img1.png
draft: false
tags: ['leetcode', 'easy', 'heapqueue']
description: 'Leetcode problem solution'
---

This blog discusses the solution to the [LeetCode problem](https://leetcode.com/problems/kth-closest-points-to-origin/description/) of finding the Kth closest points to the origin.

## Intuitive Approach

An intuitive solution involves calculating the distance of each point from the origin, storing it with the point, and then sorting the list of points based on these distances. The Kth closest point is then retrieved from the sorted list.

Here's the Python code for the intuitive approach:

```python
from math import sqrt

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        val = []
        for i in points:
            x = i[0]
            y = i[1]
            val.append((sqrt(x**2 + y**2), [x, y]))
        val.sort(key=lambda x: x[0])
        ans = [point for _, point in val]
        return ans[:k]
```

Time complexity is <mark>O(nlog(n))</mark> as we have to sort the list at the end before returning. For as we are storing the processed points and the distance inside the array of same size so the space complexity is <mark>O(n)</mark>.

> **Time Complexity: O(n log n)**
<br/>
> **Space Complexity: O(n)**

## Using Priority Queue (HeapQueue) Approach

An optimized solution utilizes a priority queue (min-heap) to efficiently find the Kth closest points without sorting the entire list. It maintains a heap of the K closest points and updates it as new points are encountered.

Here's the Python code for the heap queue approach:

```python
import heapq

class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        heap = []
        for (x, y) in points:
            dist = -(x*x + y*y)
            if len(heap) == K:
                heapq.heappushpop(heap, (dist, x, y))
            else:
                heapq.heappush(heap, (dist, x, y))
        return [(x, y) for (_, x, y) in heap]
```

So by using heap we are making the steps for sorting less, if k is less than the size of array then time it is better than the previous approach but if the k is compareable to the size of array then it is same as using previous approach this makes the time complexity <mark>O(nlog(k)</mark>. As for space complexity it is full dependent on the k value so it will be <mark>O(k)</mark>.

> **Time Complexity: O(n log K)**
<br/> 
> **Space Complexity: O(K)**

These solutions provide different approaches to solving the problem. Feel free to choose the one that best suits your needs.

