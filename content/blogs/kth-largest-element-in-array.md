---
title: "Kth Largest Element in Array"
date: 2023-12-26T12:40:37+05:30
draft: false
author: "Bibek Jha"
image: /images/blogs/post4/img1.png
description: 'Leetcode problem solution for problem number: 215'
tags: ["leetcode", "heapqueue", "medium"]
---

Today we are going to solve this [leetcode problem](https://leetcode.com/problems/kth-largest-element-in-an-array/description/). In this problem we are required to find the kth largest element in an array of number.

## Intutive Approach

This is pretty easy sum if we just sort the array and the return the kth largest element from the array. In python this is pretty easy problme cause in python list can be quried with negative number to return the elements from the end of arrray. For example <mark>List[-1]</mark> give the last element and <mark>list[-2]</mark> gives the second last element from the array and so one.

The code looks like this for the obvious approach:

```python
class Solution:
    def kthLargest(self, nums: List[int], k: int) -> int:
        nums.sort()
        return nums[-k]
```

The time complexity is <mark>O(nlog(n))</mark> as the only relevant time is taken while sorting of array. The space complexity is <mark>O(n)</mark> which is the size of array.

> **Time Complexity: O(nlog(n))**
> <br>  
> **Space Complexity: O(n)**

## Using Priority Queue

Now as we know what a priority queue is os if we just use its property then just by running the heappop command for k we can get the kth largest element from the priority queue (Max Heap).

In python heapq provides many functionality for working with heap and its different function, one such is <mark>nlargest</mark> function that takes <mark>k</mark> and a <mark>list</mark> to return the kth largest element, we will use that for the code.

The code will look like this for this qpproach.

```python
import heapq
class Solution:
    def kthLargest(self, nums: List[int], k: int) -> int:
        return heapq.nlargest(k, nums)

```

Now the time complexity is <mark>O(n)</mark> as this is the time it takes to make a list heap inplace and space complexity is same previously <mark>O(n)</mark> as space is same for the storing of list.

> **Time Complexity: O(n)**
<br>
> **Space Complexity: O(n)**

If you find any problem with this article or you just want to have chang you can contact me through the the socials.
