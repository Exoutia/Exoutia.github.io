---
title: 'Palindrome Partitioning'
date: 2024-01-05T21:36:31+05:30
draft: true
author: 'Bibek Jha'
image: /images/blogs/post10/img1.png
description: 'Leetcode problem solution for problem number: 131'
id: 10
tags: ['leetcode', 'medium', 'backtracking']
---

This is a simple backtracking sum with extra step of checking of palidrome in the way to create permutation of the word.

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        res = []
        path = []

        def dfs(i):
            if i >= len(s):
                res.append(path.copy())
                return
            for j in range(i, len(s)):
                if isPali(s, i, j):
                    path.append(s[i:j+1])
                    dfs(j+1)
                    path.pop()

        def isPali(s, i, j):
            while i < j:
                if s[i] != s[j]:
                    return False
                i, j = i + 1, j - 1
            return True
        
        dfs(0)
        return res

```
