---
title: 'N Queens'
date: 2024-01-07T07:56:50+05:30
draft: false
author: 'Bibek Jha'
image: /images/blogs/post13/img1.png
description: 'Leetcode problem solution for problem number: 51'
id: 13
tags: ['leetcode', 'hard', 'backtracking']
---

The link to problem: [leetcode/n-queens](https://leetcode.com/problems/n-queens/description/)

The problem is very famous for practicing backtracking, in this problem the questioneer is asking how to arrange <mark>n</mark> number of queens in a <mark>nxn</mark> matrix. Now if you think this can be done using backtracking where we place a queen at every position and check if the position is correct and we able to place <mark>n</mark> queens in the board then return the board with those postions.

## Backtracking
Now that the intution is clear lets see the code.
```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        state = [['.'] * n for _ in range(n)]
        res = []
        visited_cols = set()

        visited_diagonals = set()

        visited_antidiagonals = set()

        def backward(r):
            if r == n:
                res.append([''.join(row) for row in state])
                return 
            
            for c in range(n):
                diff = r - c
                sum_diag = r + c
                if not (c in visited_cols or diff in visited_diagonals or sum_diag in visited_antidiagonals):
                    visited_cols.add(c)
                    visited_diagonals.add(diff)
                    visited_antidiagonals.add(sum_diag)
                    state[r][c] = 'Q'
                    backward(r+1)

                    visited_cols.remove(c)
                    visited_diagonals.remove(diff)
                    visited_antidiagonals.remove(sum_diag)
                    state[r][c]='.'
        backward(0)
        return res

```

Now let's calculate the time complexity as for every row we have to check the posibility for that position and the position that are left so the less queens left to place the less times we have to check for correct postion so it will look some what like this <mark>n x (n - 1) x (n - 2) x ... x 1</mark>, this coresponds to <mark>O(n!)</mark> time complexity. And space complexity is <mark>O(nxn)</mark> as this is the space of board where we are adding queens.


> **Time Complexity: O(n!)**
<br/>
> **Space Complexity: O(nxn)** 
