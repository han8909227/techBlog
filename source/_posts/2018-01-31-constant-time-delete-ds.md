---
title: Leetcode 380 Constant Time Delete/Lookup DS
date: 2018-01-31 17:44:45
tags:
- interview
- data-structure
- hash map
categories:
- leetcode
---

# Insert, Delete, GetRandom O(1)
## Original Problem
{% codeblock lang:python %}
# Design a data structure that supports all following operations in average O(1) time.

# insert(val): Inserts an item val to the set if not already present.
# remove(val): Removes an item val from the set if present.
# getRandom: Returns a random element from current set of elements. Each element must have the same probability of being returned.
# Example:

# // Init an empty set.
# RandomizedSet randomSet = new RandomizedSet();

# // Inserts 1 to the set. Returns true as 1 was inserted successfully.
# randomSet.insert(1);

# // Returns false as 2 does not exist in the set.
# randomSet.remove(2);

# // Inserts 2 to the set, returns true. Set now contains [1,2].
# randomSet.insert(2);

# // getRandom should return either 1 or 2 randomly.
# randomSet.getRandom();

# // Removes 1 from the set, returns true. Set now contains [2].
# randomSet.remove(1);

# // 2 was already in the set, so return false.
# randomSet.insert(2);

# // Since 2 is the only number in the set, getRandom always return 2.
# randomSet.getRandom();

{% endcodeblock %}

<!--more-->

## Approach
The first reactions are always to build a hash map ds, but the thing about hash map is that hashing values are unique to the data stored, mening there is no way to generate a hashing value correspond to a data without knowing what the data is.
Therefore, we must use a ds with index support to get a random data out of the data set, like linked list! But the removal will be an O(n) process.
Now it's obvious we need hash map for the fast lookup time, and list for its indexing support. For this problem we must use both.
A list where all data is stored, and a hashmap to store the corresponding location(index) of that data in the list array.
To delete, we can simply find the index of the data using hashmap, and swap it with the last value in the list array, and pop it off. Constant actions = Constant time complexity


## Implmentation
{% codeblock lang:python %}
import random

class RandomizedSet(object):
    """A const time lookup/delete/get_random DS."""

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.output = []
        self.index = {}

    def insert(self, val):
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        :type val: int
        :rtype: bool
        """
        if val in self.index:
            return False
        self.index[val] = len(self.output)
        self.output.append(val)
        return True

    def remove(self, val):
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        :type val: int
        :rtype: bool
        """
        if val not in self.index:
            return False
        index = self.index[val]
        last = self.output[-1]
        self.index[last] = index
        self.output[index] = last
        self.output.pop()
        del self.index[val]
        return True

    def getRandom(self):
        """
        Get a random element from the set.
        :rtype: int
        """
        index = random.randint(0, len(self.output - 1 ))
        return self.output[index]

{% endcodeblock %}

https://leetcode.com/problems/insert-delete-getrandom-o1/