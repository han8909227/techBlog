---
layout: blog
title: Linked List Cycle problems
date: 2018-02-12 15:41:30
tags:
- interview
- linked list
- cycle detection
categories:
- leetcode
---

# Leetcode 141 Linked List Cycle
## Original Problem

{% codeblock lang:python %}

# Given a linked list, determine if it has a cycle in it.

# Follow up:
# Can you solve it without using extra space?

# example:
#1->2->3
#  |  |
#  5<-4
# return True

{% endcodeblock %}

<!--more-->

## Approach
To solve this problem let's define what is unique when we are iterating over a linked list with cycle in it.
If cycle does not exist we would eventually iterate to a null or None node, which doesn't happen if the a cycle exist in the linked list.
But that is not enough to solve the problem, we must set a stopping point for the iteration otherwise we will end up in an inf loop.
To do that let's make two pointers, one ahead of another by one node. If a cycle exist the slower one will eventually be caught up with the faster one.

## Implementation

{% codeblock lang:python %}

class LinkedList(object):
    """Simple linked list class."""

    def __init__(self, val):
        """."""
        self.next = None
        self.val = val


def detect_cycle(head):
    """LC 141."""
    slow = fast = head

    while fast and fast.next:
        slow = slow.next  # slow iterating slower pase
        fast = fast.next.next  # fast in going faster pase
        if fast == slow:
            return True  # there is an cycle
    return False


{% endcodeblock %}

https://leetcode.com/problems/linked-list-cycle/description/

***

# Leetcode 142 Linked List Cycle II
## Original Problem


{% codeblock lang:python %}

# Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

# Note: Do not modify the linked list.

# Follow up:
# Can you solve it without using extra space?

# example:
#1->2->3
#  |  |
#  5<-4
# return 3

{% endcodeblock %}


## Approach
Similarly we can use two pointers to detect a cycle in a linked list. Let's first break down where they might meet.
![alt text](https://shenjie1993.gitbooks.io/leetcode-python/linked-list-cycle.png)
A=head      B=node cycle starts(target)      C=somewhere in the cycle
If we use the same approach in the last problem, where both pointers start at A they will meet at C since the second pointer is twice as fast.
The slower pointer traverled x+y while faster pointer traverled x+y+z+y, and since we know faster pointer is twice as fast: x+y+z+y=2(x+y), meaning x=z.
At this pointer both ponter will be at C, meaning if we start another pointer from the head to traverl to B(x distance), the time it takes for the pointer at C to get to B will be the same(z distance) since we know x=z.
So, start another pointer from the head traverling at the same pase as the pointer at C, we should be able to find the cycle starting node B when they meet.

## Implementation

{% codeblock lang:python %}

class LinkedList(object):
    """Simple linked list class."""

    def __init__(self, val):
        """."""
        self.next = None
        self.val = val


def detect_cycle_ii(head):
    """LC 142."""
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:  # cycle = True
            node = head
            while node != slow:  # now the head and slow are x+z apart, target know is in between them and we knowfrom derivation we know x = z
                node = node.next  # move node through x
                slow = slow.next  # move slow through z
            return node  # node = slow = node where cycle begin
    return None

{% endcodeblock %}


https://leetcode.com/problems/linked-list-cycle-ii/description/