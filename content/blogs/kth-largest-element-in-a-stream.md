---
title: "Kth Largest Element In a Stream (Leetcode)"
date: 2023-12-23T09:06:35+05:30
author: "Bibek Jha"
image: /images/blogs/post1/img1.png
draft: false
tags: ['leetcode', 'easy', 'heapqueue']
description: 'Leetcode problem solution'
---

This is a simple software design problem in [LeetCode](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/).
So according to problem we have to create a datastruccture which will return the kth_largest element every time we add element in this datastructure.

## Intutive Approach

This soltuion can be pretty intutive just insert the new element and sort the list in reverse order and return the array the <mark>K</mark> index element.

The code would look like this:

```python
class kthLargest:
    def __init__(self, k: int, nums: list[int]):
        self.k = k
        self.nums = nums

    def add(self, n: int) -> int:
        self.nums.append(n)
        self.nums.sort(reverse=True)

        if len(self.nums) >= self.k:
            return self.nums[k-1]
        else:
            return self.nums[-1]
```

> **Time Complexity: O(nlog(n))**
<br/>
> **Space Complexity: O(n)**

## Using Priority Queue

Now the previous solution is fine and great but this can be improved by using Priority queue. In Priority queue removing smallest elements takes <mark>O(1)</mark> time. So if you read the question we just need to store the top <mark>K</mark> largest element every time a new element is added.

Now the approach should be clear that every time new data is added we remore the smallest element until the size of heap is same as k or smaller. And finally return the last element in the array.

The code look like this:

```python
import heapq

class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        # Initialize the class with k and a list of integers
        self.k = k
        self.heap = nums

        # Convert the list into a min-heap using heapq.heapify
        heapq.heapify(self.heap)

        # Keep only the k largest elements in the heap
        while len(self.heap) > self.k:
            heapq.heappop(self.heap)

    def add(self, n: int) -> int:
        # Add the new element to the heap
        heapq.heappush(self.heap, n)

        # Ensure that the heap maintains the k largest elements
        while len(self.heap) > self.k:
            heapq.heappop(self.heap)

        # Return the current kth largest element, which is the smallest in the heap
        return self.heap[0]

```

> **Time Complexity: O(n)**
<br/>
> **Space Complexity: O(n)**

Hope this helps you understand this prbolem.
