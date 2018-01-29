---
layout: blog
title: Leetcode 20 & 22 Validate & Generate Parentheses
date: 2018-01-28 15:51:07
tags:
- interview
- stack
- backtracking
- leetcode
categories:
- leetcode
---

# Validate Parentheses
## Original Problem
{% codeblock lang:python %}
# Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

# The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
{% endcodeblock %}

<!--more-->

## Approach
As many of you have seem before, this is a classic problem that utilizes stacks.
Parenthese pairs has two requirements:
- left must go before right
- the type of the closing right must match the left
For an example, '(()}' and ')()(' are not valid pairs
To satisfy the first requirement we can use indexing (dictionary to string) to ensure the closing one is the same type as opening one, and to perserve the second characteristic we can use a stack.

## Implmentation
{% codeblock lang:python %}
def valid_parentheses(s_parens):
    if not s_parens:
        return False  # if mt input
    stack = []
    left = '({['  # notice indexes matches the same type below
    right = ')}]'
    for c in s_parens:
        if c in left:
            stack.append(c)  # push left in
        elif c in right:
            temp = stack.pop()  # try to pop out the left
            if temp != left[right.index(c)]:  # if not what is suppose to closed(last left inserted)
                return False
    return True if not stack else False  # if any left still in stack(unclosed)

{% endcodeblock %}

Notice in the end we only return True when the stack is empty, this way if there is any unclosed paren in the stack it is still invalid.

https://leetcode.com/problems/valid-parentheses/


# Generate Valid Parentheses
## Original Problem
{% codeblock lang:python %}
# Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

# For example, given n = 3, a solution set is:

# [
#   "((()))",
#   "(()())",
#   "(())()",
#   "()(())",
#   "()()()"
# ]
{% endcodeblock %}

## Approach
Different then the problem above, this question is asking us to generate all possible valid combinations of parens given the number of pairs.
A common reaction is to use nested for loops, but it will be very difficultf since there are many variations not just '()()()' or '((()))'.
To solve this problem we can use a technique call backtracking, it's essentially a variation to recursion.


## Implmentation

{% codeblock lang:python %}
def generate_parenthesis(n):
    """Take n, output all valid pairs of n param."""
    ans = []
    def backtrack(s='', left=0, right=0):
        """Generate valid pairs using recursive strategy."""
        if len(s) == 2 * n:  # when a combo is made(n pairs)
            ans.append(s)
            return
        if left < n:  # condition to stop generate left (recursive)
            backtrack(s + '(', left + 1, right)
        if right < left:  # condition to stop generate right (recursive)
            backtrack(s + ')', left, right + 1)
    backtrack()
    return ans
{% endcodeblock %}

Notice the condition to stop the recursions are left < n and right < left, it restrict to be less then n, and also restricted the produciton of an right before a left
It's helpful to **draw out** the recursion call stack, it'll be much clear to you why the conditions are set up this way.

https://leetcode.com/problems/generate-parentheses/description/