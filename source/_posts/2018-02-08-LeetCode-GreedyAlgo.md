---
title: Series of Greedy Algorithm Problems
date: 2018-02-08 15:17:06
tags:
- interview
- greedy algorithms
categories:
- leetcode
---

# Leetcode 55 Jump Game

## Original Problem

{% codeblock lang:python %}
# Given an array of non-negative integers, you are initially positioned at the first index of the array.

# Each element in the array represents your maximum jump length at that position.

# Determine if you are able to reach the last index.

# For example:
# A = [2,3,1,1,4], return true.

# A = [3,2,1,0,4], return false.

{% endcodeblock %}

<!--more-->

## Approach
To clarify the question, we are given a list/array of vals. Each val represents the MAX number of jumps it can take, meaning if the val is 4 it can stop after moving 2 steps and switch onto another val for jump.
To approach this problem we must realize that we need to keep track of
- Whether or not we can reach the end with current jump
- Is there a better jump in the path of our current jump? If so switch onto that jump instead.
- Where are we as we step forward in the current jump


## Implementation

{% codeblock lang:python %}

def jump(nums):
    """Classic greedy algo."""
    idx = 0
    end = len(nums)
    longest = nums[0]  # start with the first val

    while idx <= end:  # within the list
        if longest >= end - 1:  # reached or exceed the list
            return True
        longest = max(longest, nums[idx] + longest)  # greedy part, choose better solution
        idx += 1
    return False

{% endcodeblock %}

https://leetcode.com/problems/jump-game/



# Leetcode 45 Jump Game II

## Original Problem

{% codeblock lang:python %}

# Given an array of non-negative integers, you are initially positioned at the first index of the array.

# Each element in the array represents your maximum jump length at that position.

# Your goal is to reach the last index in the minimum number of jumps.

# For example:
# Given array A = [2,3,1,1,4]

# The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

# Note:
# You can assume that you can always reach the last index.

{% endcodeblock %}

## Approach
Similar to the last problem, in this one we want to not only find out whether we can reach the end with the jumps but also return the minimum number of jump we could take. Simply put, we just got more greedy!
To approach this we would have to keep track of:
- the longest jump we can get as we step forward
- keep an variable for the max reaching distance, but not use it until it is necessary
- use the reach when the current longest cannot reach the end, means it's time for a necessary jump

## Implementation

{% codeblock lang:python %}
def jump_game_ii(nums):
    """Min step to complete the jump game."""
    length = len(nums)
    counter = 0
    longest = 0
    reach = 0

    for i in range(length):
        if longest < i:  # if i is ahead of longest (curr longest cannot complete game)
            counter += 1  # need to jump
            longest = reach  # update the longest
        reach = max(reach, nums[i] + i)  # determine what reach is for this i, either previous reach or curr val + idx
    return counter
{% endcodeblock %}

https://leetcode.com/problems/jump-game-ii/


# Leetcode 121 Best time to buy stock

## Original Problem

{% codeblock lang:python %}

# Say you have an array for which the ith element is the price of a given stock on day i.

# If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

# Example 1:
# Input: [7, 1, 5, 3, 6, 4]
# Output: 5

# max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
# Example 2:
# Input: [7, 6, 4, 3, 1]
# Output: 0

# In this case, no transaction is done, i.e. max profit = 0.

{% endcodeblock %}


## Approach
Simple and straight-forward problem, as we iterate through the list we just need to keep track of:
- the minimum price we can buy
- the maximum profit we will receive if we sell the holding stock with the current price
- update min price if there is a lower price in the list
- update max profit if we can make a better profit from any of the stock val

## Implementation

{% codeblock lang:python %}

def stock_profit(nums):
    """Also another greedy algo problem."""
    max_profit = 0
    min_price = nums[0]
    for price in nums:
        if price < min_price:
            min_price = price
        if price - min_price > max_profit:
            max_profit = price - min_price
    return max_profit

{% endcodeblock %}

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
