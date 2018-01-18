---
title: Binary Tree Boundry Traversal
date: 2018-01-17 14:40:12
tags:
- interview
- bst
- traversal
categories:
- leetcode
---


{% codeblock %}
Original Problem

# Print all edge nodes of a complete binary tree anti-clockwise.
# That is all the left most nodes starting at root,
# then the leaves left to right and finally all the rightmost nodes.
# In other words, print the boundary of the tree.

# Variant: Print the same for a tree that is not complete.


# Assume we have a binary tree below:

#     _30_
#    /    \
#   10    20
#  /     /  \
# 50    45  35
# The correct solution should print 30, 10, 50, 45, 35, 20.


{% endcodeblock %}


To start we must understand the question, it's asking us to traverse a binary tree
counter-clockwise and only return the edge nodes.

### Approach

This problem is easier to break it down to multiple parts since not a single type
of common traversal would do traversal clockwise or counter-clockwise

