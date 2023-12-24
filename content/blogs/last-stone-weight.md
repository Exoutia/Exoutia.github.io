---
title: 'Last Stone Weight'
date: 2023-12-24T07:46:57+05:30
draft: false
author: 'Bibek Jha'
image: /images/blogs/post2/img1.png
tags: [
    'leetcode',
    'easy',
    'heapqueue'
]
---

Link to the question: [LeetCode/Last-stone-weight](https://leetcode.com/problems/last-stone-weight/description/)

In this problem, you are given an array of integers representing the weights of stones. The goal is to simulate a game where, at each turn, the two heaviest stones are selected and either both are destroyed (if they have the same weight) or the lighter stone is destroyed, and the heavier one's weight is updated. The process repeats until there is at most one stone left, and you need to return the weight of the last remaining stone or 0 if there are no stones left.

## Intutive Approach

The forcefull approach would be to find the two largest stones, smash them and insert their value into the list again. This will be done until the length of list of stones is less than one.
You can then make this somewhat good by sorting the array and then pick the two largest element from the last and insert them again into the array and again sort the array to make it work in next iteration like this.

```python
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # Step 1: Sort the list of stones in ascending order
        stones.sort()

        # Step 2: Continue the process until there are at most two stones remaining
        while len(stones) > 1:
            # Step 3: Select the two heaviest stones
            larger = stones.pop()       # Get the weight of the larger stone
            smaller = stones.pop()      # Get the weight of the smaller stone

            # Step 4: Process the stones based on their weights
            if larger == smaller:
                # Both stones are destroyed if they have the same weight
                continue
            else:
                # Create a new stone with weight equal to the difference of the two stones' weights
                stones.append((larger - smaller))

            # Step 5: Sort the stones again in ascending order
            stones.sort()

        # Return the weight of the last remaining stone or 0 if there are no stones left
        return stones[0] if stones else 0

```

Now analyze the time and space complexity for the solution. The sorting takes <mark>O(nlog(n))</mark> and the sorting is done at every iteration which is running for n times as the length of the stones list this implies that for n number of stones the sorting is done <mark>n</mark>. By calculating the time complexity comes as <mark>O(n<sup>2</sup>log(n))</mark>.

For space complexity is constant at no step we are using the any new array and every operation done in same array as stones so it will come to <mark>O(n)</mark>.

> </mark>Time Complexity: O(n<sup>2</sup> log(n))
> <br>
> Space Complexity: O(n)

## Max Priority Queue

Now we can optimize the solution by observing the steps and what could we change different. First step while optimizing the code usually check for the repeating steps and eleminate those by using some tricks or data structures.

In the previous solution it is obvious we are sorting the list after every iteration if we could just add the stones into the list and it will arrange itself in the correct order we could save so much time. 

To be fair there is a datasctructure which does that named as "Priority Queue" with two variants "Min Priority Queue" and "Max Priority Queue".

A max-priority queue is a data structure that maintains a collection of elements with assigned priorities and allows efficient retrieval of the element with the highest priority. The element with the maximum priority is always dequeued first.

We are going to use "Max Priority Queue" to be mroe specific ( but python <mark>heapq</mark> does not support max-priority queue so we just multiply the <mark>-1</mark> to make the largest element smallest and while getting the element we just multiply with <mark>-1</mark> again this will ensure the calculation is correct at every step). By using this when we call two times <mark>heappop</mark> we will get two largest element and when inserting the new element the datastructure will be correctly arranged.

Getting the largest element in Max Priority Queue takes <mark>O(1)</mark> time and insertion takes <mark>O(log(n))</mark>.

```python 

import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # Initialize a max heap, push negation of stone weights, and update heap after each smashing operation
        heap = []
        for i in stones:
            heapq.heappush(heap, -1 * i)
        while len(heap) > 1:
            y = -1 * heapq.heappop(heap)
            x = -1 * heapq.heappop(heap)
            if x == y:
                continue
            else:
                heapq.heappush(heap, -1 * (y - x))
        return heap[0] * -1 if heap else 0  # Return the weight of the last remaining stone or 0 if no stones left
```
Now analyze the time and space complexity for the solution. The heap operations take <mark>O(log n)</mark>, and the loop iterates until there is at most one stone left, resulting in a total time complexity of <mark>O(nlog(n))</mark> due to the heap operations. The space complexity is O(n) as the heap stores the negation of stone weights.

> Time Complexity: O(nlog(n))
<br>
> Space Complexity: O(n)
