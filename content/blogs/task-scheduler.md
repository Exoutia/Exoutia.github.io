---
title: "Task Scheduler"
date: 2023-12-27T14:42:54+05:30
draft: false
author: "Bibek Jha"
image: /images/blogs/post5/img1.png
description: 'Leetcode problem solution for problem number: 621'
id: 5
tags: ["leetcode", "heapqueue", "queue", "medium"]
---

Today we are going to solve this [leetcod/task-scheduler](https://leetcode.com/problems/task-scheduler/description/). This is a good problem and would need some thinking to solve it thorughly. 

## Heapqueue Approach
In the question one had to find the least time a computer would take to complete some tasks, while completing task computer has to take some time before it can do the same task again so either do another task or do nothing for that unit of time. We are asked to find the least time it would take to complete all the task.

To solve this question we will take a maxHeap (max-priority-queue) why we will do this just imagine what would be best way to arrange solve the task that we can do other task while its in cooldown period obviously the one with the most count cause then after other task we can take those task not worry about wasting time while less count task is in cooldown period. 

![maxHeap and queue visualisation](/images/blogs/post5/img2.png) 

The algorithm is pretty simple:
1. Create a <mark>maxHeap</mark> from the count of tasks provided by the problem.
2. Create a <mark>queue</mark> to store the updated count after one task is done and time when when its in cooldown period.
3. Create the <mark>time</mark> variable to start the count when the task is being done by computer.
4. start while loop until any one <mark>queue</mark> or <mark>maxHeap</mark> contains task to complete.
5. inside the loop increase the <mark>time</mark> by 1.
6. check if the <mark>maxHeap</mark> contains any task to do. If there is pop it minus one from the count and calculate the cooldown for it by adding the current <mark>time</mark> and the cooldown variable <mark>n</mark>. Then insert both variable inside the <mark>queue</mark>. I will not do it if the count of any task become 0 then it will just be skipped.
7. Now check if <mark>queue</mark>'s top element cooldown time is equal to the current <mark>time</mark> variable. If it is pop it and insert into the <mark>maxHeap</mark>.
8. repeat step 4 to 7 until both <mark>queue</mark> and <mark>maxHeap</mark> is empty.
9. When loop stops return the <mark>time</mark> variable.

Now the code look like this. (as python heapq library only contains min-heap we i am going to treat those number in count as negative and instead of minus 1 from tasks count I will add it everything else will be same and when the task number reaches 0 will not add it inside the queue.)

```python
import heapq
from collections import Counter, deque
from typing import List


class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        maxHeap = [-i for i in Counter(tasks).values()]
        heapq.heapify(maxHeap)
        time = 0
        queue: deque[tuple[int, int]] = deque()
        while maxHeap or queue:
            time += 1
            if maxHeap:
                task_count = 1 + heapq.heappop(maxHeap)
                cooldown = n + time
                if task_count < 0:
                    queue.append((task_count, cooldown))
            if queue and queue[0][1] == time:
                heapq.heappush(maxHeap, queue.popleft()[0])
        return time        

```
Now lets see whats the time complexity, for making a heap we take <mark>O(n)</mark> (<mark>n</mark> is the number of tasks) time and every other operation is <mark>O(1)</mark> (the insertion in queue)  or <mark>O(log(n))</mark> (the insertion in heap) but in worst case (where all the task is of same type) the loop has to theoritically run for <mark>O(n * m)</mark> (where <mark>m</mark> is the cooldown time). And space complexity is <mark>O(n)</mark> cause space taken by heap is <mark>O(26)</mark> (since tasks can be only upper case english alphabet letters) which corresponds to <mark>O(1)</mark> so it is not included into the space complexity and we only count the space taken by taks list.

> **Time Complexity: O(n*m)** 
<br />
> **Space Complexity: O(n)**

If you got any issue or just want to talk to me about something ping me up in my socials.
