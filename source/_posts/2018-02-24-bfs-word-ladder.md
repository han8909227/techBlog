---
layout: blog
title: Word Ladder
date: 2018-02-24 15:15:15
tags:
- interview
- bfs
- word ladder
categories:
- leetcode
---

# Leetcode 127 Word Ladder
## Original Problem

{% codeblock lang:python %}
# wordList = ["hot","dot","dog","lot","log","cog"]
# As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
# return its length 5.

# Note:
# Return 0 if there is no such transformation sequence.
# All words have the same length.
# All words contain only lowercase alphabetic characters.
# You may assume no duplicates in the word list.
# You may assume beginWord and endWord are non-empty and are not the same.

{% endcodeblock %}

<!--more-->

## Approach
We are trying to turn a word, changing only 1 charater at a time to become the end word. And return the shortest path to that transformation. So we can visualize using a tree structure graph:
![alt text](https://shenjie1993.gitbooks.io/leetcode-python/leetcode-word-ladder.png)
All words during the transformation, including the end word are children of the initial word. We can also conclude:
- we must use breath-first-search approach becuase we want to find as much path to the end node(word) as possible, to compare which one is the shortest.
- the level of the node reflects the number of changes (i.e length of the transformation)
- words appeared in the previous level shouldn't appear in the following levels, or the nodes should be unique words.
- to reduce the time complexity we can find one path (must with same path length) to a same word instead of all. For an example, in the tree above both bit and him can turn into bim, we can only find bit=>bim and no need to find him=>bim since they offer the same path length, and path length is all we care about.
This would make more sense once you follow the logic of the codes.

## Implementation

{% codeblock lang:python %}


def bfs(begin, end, word_list):
    """LC127 with bfs
    type str: begin
    type str: end
    type set: word_list
    return int.
    """
    word_list.add(end)
    depth = 0
    curr_level = [begin]
    n = len(begin)
    next_level = []

    while curr_level:
        for val in curr_level:
            if val == end:
                return depth

            for i in range(n):
                for l in 'abcdefghijklmnopqrstuvwxyz':
                    w = val[:i] + l + val[i + 1:]  # assess every combonations
                    if w in word_list:  # if it's valid
                        word_list.remove(w)  # ensure not use it again
                        next_level.append(w)  # w become part of transfromation
        depth += 1
        curr_level = next_level
        next_level = []
    return 0


if __name__ == "__main__":
    assert bfs("hit", "cog", {"hot", "dot", "dog", "lot", "log"}) == 5

{% endcodeblock %}

https://leetcode.com/problems/word-ladder/description/
