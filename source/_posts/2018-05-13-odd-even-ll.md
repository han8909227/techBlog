---
layout: blog
title: Odd Even Linked List
date: 2018-05-13 15:00:00
tags:
- interview
- linked list
categories:
- leetcode
---

# Leetcode 348 Odd even Linked List
## Original Problem

{% codeblock lang:python %}
# Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

# You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

# Example:
# Given 1->2->3->4->5->NULL,
# return 1->3->5->2->4->NULL.

# Note:
# The relative order inside both the even and odd groups should remain as it was in the input. 
# The first node is considered odd, the second node even and so on ...
{% endcodeblock %}

<!--more-->

## Approach
This problem require us to re-order a linked list by the node number, all odd nodes follow by all even nodes in the original linked list.
Although this seems complicated with a single pass, it can be done if we break down the linked list into two parts, an even part and an odd part.
With the two parts each contain nodes categorized with even or odd. Which allows us to simply concat these two linked list to form the final linked list, which will satisfy the requirement of this proble.
For details try to follow the implementation below.


## Implementation

{% codeblock lang:python %}

class LinkedList(object):
    """Simple linked list class."""

    def __init__(self, val):
        """."""
        self.next = None
        self.val = val


def odd_even_ll(head):
    """LC 328."""
    odd = LinkedList(None)
    even = LinkedList(None)

    # mark down the dummy nodes
    odd_head = odd
    even_head = even
    count = 1

    while head:
        # form even node ll
        if count % 2 == 0:
            even.next = head
            even = even.next

        # form odd node ll
        else:
            odd.next = head
            odd = odd.next

        # iterate & break up original node's link
        temp = head.next
        head.next = None
        head = temp
        count += 1

    # concat odd ll to even ll
    odd.next = even_head.next

    # return odd ll head (original head)
    return odd_head.next

if __name__ == '__main__':
    ll = LinkedList(1)
    ll.next = LinkedList(2)
    ll.next.next = LinkedList(3)
    ll.next.next.next = LinkedList(4)
    ll.next.next.next.next = LinkedList(5)
    ll.next.next.next.next.next = None

{% endcodeblock %}

https://leetcode.com/problems/odd-even-linked-list/description/