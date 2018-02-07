---
title: Leetcode Unique Path I & II
date: 2018-02-06 16:17:43
tags:
- interview
- dfs
- dynamic programming
categories:
- leetcode
---

# Unique Path I Leetcode #62

## Original Problem
![alt text](https://leetcode.com/static/images/problemset/robot_maze.png)
{% codeblock lang:python %}
# A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

# The robot can only move either down or right at any point in time.
# The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

# How many possible unique paths are there?

{% endcodeblock %}


<!--more-->

## Approach

The problem state thats the robot may only move from down or to the right to get to the bottom-right corner, this makes things easier.
For an example, I have a 2x2 matrix the only way I can get from top-left corner to bottom-right corner is 2. Which is the total number of ways I can get to 0,1 and 1,0, the top and left of 2,2 (the destination). Hence we can derive the equation A[i][j] = A[j-1][i] + A[j][i-1], to represent the total number of ways to get to a location in the matrix.
We can solve this problme using depth-frist search, go through all possible path from the end to the start. But the draw back is that with dfs the time complexity will be O(N^4) which will time out on large matrix.
To solve that we can use dynamic programming instead, to approach the problem from start head to the end. The idea is to make an identical size matrix filled with 1s, and ignore the edges start traversal from 1,1 since there will be only 1 way to get through the edge spots. Similarly, filled out the possible ways of getting into each spot in that matrix by the formula above (left + top combination). In the end, the bottom-right spot should contain the total number of ways to get to that spot from the beginning.



## Implementation

{% codeblock lang:python %}

def unique_path(m, n):
    """LC62 with dynamic programming."""
    dp = [[1 for _ in range(n)] for _ in range(m)]
    for i in range(1, n):
        for j in range(1, m):
            dp[j][i] = dp[j - 1][i] + dp[j][i - 1]
    return dp[m - 1][n - 1]  # m,n is size index starts at zero


def unique_path_dfs(m, n):
    """LC62 dfs approach."""
    if m < 1 or n < 1:  # stop condition
        return 0
    if m == 1 and n == 1:  # reward condition
        return 1
    return unique_path_dfs(m - 1, n) + unique_path_dfs(m, n - 1)  # to final point must be the total way from top and left combined


{% endcodeblock %}

https://leetcode.com/problems/unique-paths/


# Unique Path II Leetcode #63

## Original Problem
{% codeblock lang:python %}
# Follow up for "Unique Paths":

# Now consider if some obstacles are added to the grids. How many unique paths would there be?

# An obstacle and empty space is marked as 1 and 0 respectively in the grid.

# For example,
# There is one obstacle in the middle of a 3x3 grid as illustrated below.

# [
#   [0,0,0],
#   [0,1,0],
#   [0,0,0]
# ]
# The total number of unique paths is 2.

# Note: m and n will be at most 100.


{% endcodeblock %}
<!--more-->

## Approach
The idea is similar to the previous problem, but added the ability to have obstacles.
We can use dynamic programming as well, filling out an all 1s array as we go. But we need to beware to escape the obstacles. To do that we initialize the matrix with all zeros, fill out the edge spots with 1s except for where obstacles are.
Then we may start the traversal similar to last problem, but escape all spots with 1s in the original matrix since they are obstacles.


## Implementation

{% codeblock lang:python %}

def unique_path_ii(nums):
    """LC63 Dynamic programming."""
    if nums[0][0] == 1:  # cannot start
        return 0
    m = len(nums)
    n = len(nums[0])
    dp = [[0 for _ in range(n)] for _ in range(m)]
    dp[0][0] = 1  # set the start point
    for i in range(1, m):  # change edges since path traversal starts 1,1
        dp[i][0] = dp[i - 1][0] if nums[i][0] == 0 else 0
    for j in range(1, n):  # change edges since path traversal starts 1,1
        dp[0][j] = dp[0][j - 1] if nums[0][j] == 0 else 0

    for i in range(m):  # path traversal
        for j in range(n):
            if nums[i][j] == 1:  # if cannot be passed, erase that possible route
                dp[i][j] = 0
            else:  # if can be passed, accumualte from previous(from top and left)
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
    return dp[m - 1][n - 1]  # the total number of routes

{% endcodeblock %}

https://leetcode.com/problems/unique-paths-ii/