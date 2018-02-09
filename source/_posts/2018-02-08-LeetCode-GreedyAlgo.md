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
To approach this problem we must realize that we need to keep track of:
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








{% codeblock lang:python %}
{% endcodeblock %}

{% codeblock lang:python %}
{% endcodeblock %}

{% codeblock lang:python %}
{% endcodeblock %}

{% codeblock lang:python %}
{% endcodeblock %}

{% codeblock lang:python %}
{% endcodeblock %}