---
title: Binary Tree Boundry Traversal
date: 2018-01-17 14:40:12
tags:
- interview
- binary tree
- traversal
- leetcode
categories:
- leetcode
---

{% codeblock lang:python %}
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

<!--more-->

To start we must understand the question, it's asking us to traverse a binary tree
counter-clockwise and only return the edge nodes.

** Approach **
This problem is easier to break it down to multiple parts since not a single type
of common traversal would do traversal clockwise or counter-clockwise.
In order to traversal counter-clockwise we need
- traverse just left side children in order
- traverse all bottom leaf from left to right(across)
- traverse just right side children in reverse order

In the end we can join them together to form the counter-clock traversal path of the tree.

Code as follow, notice how we reverse the right traversal
{% codeblock lang:python%}
def boundry_traversal(head):
    """Return boundry traversal of a bt."""
    left = dfs_left_nodes(head)[:-1]  # don't want tail, will traversed in bottom
    bottom = dfs_children_only(head)
    right = dfs_right_nodes(head)[::-1]  # reverse to match counter clock pattern
    right = right[:-1]  # don't want tail, traversed in bottom
    right = right[1:]  # don't want head, traversed in left
    return left + bottom + right
{% endcodeblock %}

To traverse the all left nodes from root, a simple left dfs would do
{% codeblock lang:python %}
def dfs_left_nodes(node):
    """Return left nodes, with head reserve order."""
    nodes = []
    if node:
        nodes.append(node.data)
        nodes.extend(dfs_left_nodes(node.left))  # find all left nodes
    return nodes
{% endcodeblock %}

And similary to traverse all right node in order which we reverse later
{% codeblock lang:python %}
def dfs_right_nodes(node):
    """Return right nodes, no head no tail, reverse order."""
    nodes = []
    if node:
        nodes.append(node.data)
        nodes.extend(dfs_right_nodes(node.right))  # find all right nodes
    return nodes
{%endcodeblock%}

To traverse only the leafs
{% codeblock lang:python %}
def dfs_children_only(node):
    """Traverse only last childrens."""
    nodes = []
    if node:
        if not node.left and not node.right:  # only append when reaching leafs
            nodes.append(node.data)
        nodes.extend(dfs_children_only(node.left))
        nodes.extend(dfs_children_only(node.right))
    return nodes
{% endcodeblock %}