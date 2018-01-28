---
title: LeetCode No.200 Island Count
date: 2018-01-28 15:28:48
tags:
- interview
- bfs
- matrix
- leetcode
categories:
- leetcode
---

## Orginal Problem
{% codeblock lang:python %}
# Given a 2D array binaryMatrix of 0s and 1s, implement a function getNumberOfIslands that returns the number of islands of 1s in binaryMatrix.

# An island is defined as a group of adjacent values that are all 1s. A cell in binaryMatrix is considered adjacent to another cell if they are next to each either on the same row or column. Note that two values of 1 are not part of the same island if they’re sharing only a mutual “corner” (i.e. they are diagonally neighbors).

# Explain and code the most efficient solution possible and analyze its time and space complexities.

# Example:

# input:  binaryMatrix = [ [0,    1,    0,    1,    0],
#                          [0,    0,    1,    1,    1],
#                          [1,    0,    0,    1,    0],
#                          [0,    1,    1,    0,    0],
#                          [1,    0,    1,    0,    1] ]

# output: 6 # since this is the number of islands in binaryMatrix.
#           # See all 6 islands color-coded below.

{% endcodeblock %}
<!--more-->

## Approach
The problem is asking us to identify the number of islands or cluster of 1s in a binary matrix. If we simply count the number of 1s it'll be difficult to track which 1 belong to which cluster and thus will not give accurate answer. The depth first traversal approach is one that's easy to understand, we'll loop over the entire matrix and if the number is an 1, we will utlize dpeth first traversal to find all 1s linked or inter-linked to the 1 that initiated the dfs.

## Implementation

First, we must create a function to loop over the matrix
{% codeblock lang:python %}
def count_island(bm):  # bm: binary matrix
    l = len(bm[0])  # bm width
    h = len(bm)  # bm height
    if not h:
        return 0  # if no bm
    for r in range(h):
        for c in range(l):
            if bm[r][c]:  # if true, or val is 1
                count += 1  # new cluster
                dfs(bm, r, c)  # erase all 1s in this cluster
    return count

{% endcodeblock %}

Following we can write a depth first traversal function to traverse all 1s in a cluster.

{% codeblock lang:python %}
def dfs(bm, r, c):
    l = len(bm[0])
    h = len(bm)
    if r < 0 or c < 0 or r >= h or c >= l or bm[r][c] == 0:
        return  # condition to stop the recursion or traversing
    bm[r][c] = 0  # set all 1s in the cluster to 0, prevent being found in the future
    dfs(bm, r - 1, c)
    dfs(bm, r + 1, c)
    dfs(bm, r, c - 1)
    dfs(bm, r, c + 1)

{% endcodeblock %}


https://leetcode.com/problems/number-of-islands/

