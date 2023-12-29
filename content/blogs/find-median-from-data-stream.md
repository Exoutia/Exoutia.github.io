---
title: 'Find Median From Data Stream'
date: 2023-12-29T10:53:07+05:30
draft: false
author: 'Bibek Jha'
image: /images/blogs/post7/img1.png
description: 'Leetcode problem solution for problem number: 295'
tags: ['leetcode', 'heapqueue', 'hard']
---
The link to problem is [Leetcode/find-median-from-data-stream](https://leetcode.com/problems/find-median-from-data-stream/description/) 

This is hard problem but it is somewhat easy compared to some other hard problems. It is only easy if you know data-structures well enough. In this problem you are asked to create class which has two methods one for adding a integer, other function is used to get median in the ordered list made up of elements added previously in the list.

## Heapqueue Approach
Now this problem is hard cause we have to get median in <mark>O(1)</mark> constant complexity. So if we can make a datas-tructure that will make the list always sorted in comparable time then it should be fine. To get median if we can just get two middle element in even number of elements of array. If you think carefully the one data-structure that can sort elements automatically, is heap and if we divide the array in two parts with <mark>min-heap</mark> and <mark>max-heap</mark>. Where <mark>max-heap</mark> will store two left side elemnts and <mark>min-heap</mark> for right side elements. Both sides should have approxiamte size so that we can get the median from larger side, when the array is odd length.

Why we use <mark>max-heap</mark> for left side and <mark>min-heap</mark> right cause median is calculated using middle two elements and <mark>max-heap</mark> will give maximum element and <mark>min-heap</mark> will give minimum element. 

Now we can see the code to get better idea about the solution:


```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small_heap = []
        self.large_heap = []

    def addNum(self, num: int) -> None:
        if self.large_heap and num > self.large_heap[0]:
            heapq.heappush(self.large_heap, num)
        else:
            heapq.heappush(self.small_heap, -num)

        if len(self.small_heap) > len(self.large_heap) + 1:
            heapq.heappush(self.large_heap, -heapq.heappop(self.small_heap))
        elif len(self.large_heap) > len(self.small_heap):
            heapq.heappush(self.small_heap, -heapq.heappop(self.large_heap))

    def findMedian(self) -> float:
        if len(self.small_heap) > len(self.large_heap):
            return -self.small_heap[0]
        elif len(self.small_heap) < len(self.large_heap):
            return self.large_heap[0]
        return (-self.small_heap[0] + self.large_heap[0]) / 2.0


```
Time complexity for addNum is <mark>O(log(n))</mark> and findMedian is <mark>O(1)</mark> and if you think number of times the number is added to the data-structure then it becomes the <mark>O(nlog(n))</mark>. The space complexity is <mark>O(n)</mark> which is due to storing the <mark>n</mark> elements in two different list which will add up to <mark>n</mark>. 

> **Time Complexity: O(nlog(n))** 
<br />
> **Space Complexity: O(n)** 


