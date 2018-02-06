---
title: Leetcode 146 LRU Cache
date: 2018-02-02 11:42:57
tags:
- interview
- data-structure
- LRU cache
categories:
- leetcode
---

# LRU Cache

## Original Problem
{% codeblock lang:python %}

# Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

# get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
# put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

# Follow up:
# Could you do both operations in O(1) time complexity?

# Example:

# LRUCache cache = new LRUCache( 2 /* capacity */ );
# cache.put(1, 1);
# cache.put(2, 2);
# cache.get(1);       // returns 1
# cache.put(3, 3);    // evicts key 2
# cache.get(2);       // returns -1 (not found)
# cache.put(4, 4);    // evicts key 1
# cache.get(1);       // returns -1 (not found)
# cache.get(3);       // returns 3
# cache.get(4);       // returns 4


{% endcodeblock %}
<!--more-->

## Approach
This is a classic Google interview probem, and frequently used in user-orientied application implementations.
In case the problem is not clear, we are designing a data structure that can hold a set amount of data, once the data limit is reached the oldest/first-inserted data will be erased from the data base since it's considered 'lease used'. With the same idea if we get or call a data no matter when it was inserted it will be now the newest or most recent used data.
In summary, this ds needs to be able to set a size and push out old data if size is reached. That sounds like a doubly linked list! This ds also needs to be able to retrive a data point and put it front of the list if it is called upon, sounds like we also need a dictionary or hash map to keep track of each node.
So our ideas are:
- each data is a dll node with pre and next pointer
- inserted node will be added to the head of the dll, and it'll be remembered by our dictionary (node.val:node)
- get will retrive that node from the dictionary and reassign it's neighor's pointer to remove it from dll and insert again
- there will always be a head and a tail node (null nodes) to better keep track of the head and tail even in zero size.


## Implementation
{% codeblock lang:python %}
class Node(object):
    """Simple Node classs for dll."""

    def __init__(self, key, value):
        """."""
        self.key = key
        self.value = value
        self.prev, self.next = None, None


class LRUCache(object):
    """."""

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.size = 0
        self.capacity = capacity
        self.dict = {}
        self.head, self.tail = Node(-1, -1), Node(-1, -1)
        self.head.next, self.tail.prev = self.tail, self.head

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if key in self.dict:
            node = self.dict[key]
            self._remove(node)
            node.value = value
            self._insert(node)
        else:
            if self.size == self.capacity:
                discard = self.tail.prev
                self._remove(discard)
                del self.dict[discard.key]
                self.size -= 1
            node = Node(key, value)
            self.dict[key] = node
            self._insert(node)
            self.size += 1

    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key not in self.dict:
            return -1
        node = self.dict[key]
        self._remove(node)
        self._insert(node)
        return node.value

    def _insert(self, node):
        """
        :type node: Node
        :rtype: void
        Insert after head: head is always -1 node
        """
        node.prev, node.next = self.head, self.head.next
        self.head.next.prev = node
        self.head.next = node

    def _remove(self, node):
        """
        :type node: Node
        :rtype: void
        Remove node from the dll (always in the middle)
        """
        node.prev.next = node.next
        node.next.prev = node.prev
        node.next, node.prev = None, None

{% endcodeblock %}


https://leetcode.com/problems/lru-cache/description/
