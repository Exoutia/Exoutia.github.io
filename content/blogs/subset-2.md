---
title: 'Subset 2'
date: 2024-01-02T20:54:43+05:30
draft: false
author: 'Bibek Jha'
image: /images/blogs/post8/img1.png
description: 'Leetcode problem solution for problem number: 90'
tags: ['backtracking', 'medium', 'leetcode']
---
Today I solved this leetcode problem [leetcode/subsets-ii](https://leetcode.com/problems/subsets-ii/description/), before solving this question one should solve the [leetcode/subset](https://leetcode.com/problems/subsets/).

## Backtracking 
In this problem we need to find the powerset of the list of number given. The catch is that the list of numbers can contain the duplicates but the ans set shouldn't contain any duplicates. To solve the problem we can use backtrackint where at every step we either include the number or not. If we do this we can solve the subsets problem but subset has the condition to not include the duplicate. To solve this at every step we can make sure that we don't include the duplicate step that we already included in the include side. This is because at every other step where the duplicate is added will include the combination for that number with all the arrangement so we just need to skip that duplicate number altogether where we skipping the numbers. This can be done using the sorting of number altogether.
To better understand let's see the below diagram.

![state space tree for the prbolem with skipping of duplicate number on the skipping side of branches](/images/blogs/post8/img2.png) 

Now let us see the code to better understand this approach.

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        def dfs(i, sub):
            if i == len(nums):
                res.append(sub.copy())
                return
            sub.append(nums[i])
            dfs(i+1, sub)

            sub.pop()
            while i + 1 < len(nums) and nums[i] == nums[i+1]:
                i += 1
            dfs(i+1, sub)
        dfs(0, [])
        res
        return res
```
Time complexity <mark>n2<sup>n</sup></mark> this is due to the time complexity for generating the list of every arrangement we are taking 2 descision of either including the number or not which is happening for every element that's why the time complexity is so huge. Space complexity is same.

> **Time Complexity: n2<sup>n</sup>** 
<br/>
> **Space Complexity: n2<sup>n</sup>** 


