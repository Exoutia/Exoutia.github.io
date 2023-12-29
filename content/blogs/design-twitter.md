---
title: 'Design Twitter'
date: 2023-12-28T14:40:54+05:30
draft: false
author: 'Bibek Jha'
image: /images/blogs/post6/img1.png
description: 'Leetcode problem solution for problem number: 355'
tags: ['leetcode', 'hashmap', 'heapqueue', 'medium', 'queue']
---
The link to question is [lettcode/design-twitter](https://leetcode.com/problems/design-twitter/description/). 

The question is asking us to design a simple twitter like class. It has four functions:
    - To create a post.
    - To follow another user.
    - To unfollow any user.
    - To get newsfeed which comprises of ten recent post from the people user is following and himself.

This question is somewhat advanced level to solve it one should already be adept in other datastructures like array and have some idea about sorting. Before doing this you can solve this [question](https://leetcode.com/problems/merge-k-sorted-lists/description/) first. 

Now that the basic gist of question is clear, let's solve it. let's break it down.
## Twitter Design

### To follow users
Let's start thinking, this function takes the <mark>followerId</mark> and <mark>followeeId</mark> and we need to connect two id together. Now one user can have many followers and user can also follow many other users. 

![showing the users and followers connections](/images/blogs/post6/img2.png) 

To resolve this problme one can use <mark>hashmap</mark> where every <mark>followerId</mark> is key and which will sotre a set with every <mark>followeeId</mark>. This way every time new <mark>followeeId</mark> is added to specific <mark>followerId</mark> it will solve all the problem.

### To unfollow users
In previous section we made the hashmao so to unfollow just remove the <mark>followeeId</mark> from the set of <mark>followekId</mark>.

### To create new post
Now we can store the tweets in hasmap but with key as <mark>userId</mark> and tweets can be stored into a <mark>queue</mark>. This way when we retrive the posts accordingly to the order they are created.

### To create newsfeed
To create news feed we will just merge the arrays gotten from the different users from his followers List according to the hashmap. Just like <mark>merging k sorted list</mark>.


Now let's see the code.

```python

class Twitter:
    def __init__(self):
        self.count = 0
        self.tweetMap = defaultdict(list)  # userId -> list of [count, tweetIds]
        self.followMap = defaultdict(set)  # userId -> set of followeeId

    def postTweet(self, userId: int, tweetId: int) -> None:
        self.tweetMap[userId].append([self.count, tweetId])
        self.count -= 1

    def getNewsFeed(self, userId: int) -> List[int]:
        res = []
        minHeap = []

        self.followMap[userId].add(userId)
        for followeeId in self.followMap[userId]:
            if followeeId in self.tweetMap:
                index = len(self.tweetMap[followeeId]) - 1
                count, tweetId = self.tweetMap[followeeId][index]
                heapq.heappush(minHeap, [count, tweetId, followeeId, index - 1])

        while minHeap and len(res) < 10:
            count, tweetId, followeeId, index = heapq.heappop(minHeap)
            res.append(tweetId)
            if index >= 0:
                count, tweetId = self.tweetMap[followeeId][index]
                heapq.heappush(minHeap, [count, tweetId, followeeId, index - 1])
        return res

    def follow(self, followerId: int, followeeId: int) -> None:
        self.followMap[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        if followeeId in self.followMap[followerId]:
            self.followMap[followerId].remove(followeeId)

```
Hope this helps you. If you got any message for me just ping me using my socials.





