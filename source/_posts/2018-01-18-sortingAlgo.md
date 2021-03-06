---
title: Difference in common sorting algorithms
date: 2018-01-18 17:58:20
tags:
- interview
- sorting
- algorithms
categories:
- Algorithms
---


# Sorting Algorithms
***
## Bubble Sort
### Psudo Code
{% codeblock lang:python %}
While True
  changed = False
  for all num in nums
        if num > next_num
            switch them
            changed = True
    if not changed:
        return nums
{% endcodeblock %}

### Idea
Swap pairs again and again until everything is in order.
Worse case (reverse sorted list) will have to loop the list N times

### Time Complexity
**Worse**: O(N^2)
**Best**: O(N)

<!--more-->

***
## Insertion Sort
### Psudo Code
{% codeblock lang:python %}
for i in range(1, len(nums)):
    curr = nums[i]
    pos = i
    while pos > 0 and nums[pos - 1] >  curr:
        swap nums[pos] with nums[pos -1]
        pos -= 1  # heading toward head
    nums[pos] = curr  # found sorted place
return nums
{% endcodeblock %}

### Idea
For every value starting at second number in the list, until the end
If it is greater than the value before it swap them, all the way to
the sorted plac.

### Time Complexity
**Worse**: O(N^2)
**Best**: O(N)

***
## Merge Sort
### Psudo Code
{% codeblock lang:python %}
def merge_sort(nums):
    if len(nums) <  2:  # stop recurse condition
        return nums
    mid = len(nums) // 2
    left = ms(nums[:mid])  # left of mid
    right = ms(nums[mid:])  # right of mid
    return ms(left, right)

def ms(left, right):
    result = []
    while left and right:  # both has values
        if left[0] <= right[0]:  # if head is l < r
            append left[0]
            left = left[1:]  # cut left head
        else:
            append right[0]
            right = right[1:]
    while left:  # when list is odd len
        append left[0]
        cut left head
    while right:
        append right[0]
        cut right head
    return result

{% endcodeblock %}

### Idea
Break down the list to left and right, min length of 2.
Recursively call back the broken list to merge them together,
by putting back the initial vlaue from the broken left and right lists,
by comparing their value(0 index) which causus the merged list to be sorted.
In the end the last merged list will be all sorted.
Each merge operation causes O(logn) and there needs to be n merges
so mathmatically logn + longn ... n times is O(nlogn), therefore the time
complexity is O(nlogn) no matter how unsorted or sorted the list is.

### Time Complexity
**Worse**: O(Nlog(N))
**Best**: O(Nlog(N))

***
## Radix Sort
### Psudo Code
{% codeblock lang:python %}
def radix(nums):
    nums = stringfy(nums)
    max_val = len of longest number
    q_set = [set of 10 Queues]
    for i in range(1, len(max_val) + 1):  # range is important since we loop backward
        populate_set(nums, i, q_set)  # for each number in list
        nums = dequeue_set(q_set)
    return intergerified nums

def populate_set(nums, i, q_set):
    for num in nums:
        insert the num into q_set[val of num last digit]

def dequeue_set(q_set):
    temp = []
    for q in q_set:
        for _ in range(len(q)):  # all val in single q
            push(q.dequeue) into temp
    return temp

{% endcodeblock %}

### Idea
Radix sort employees the bin sorting approach to sort a collection of values.
First each number we put it's digit starting the last one into a collection of queues
which are in ordered, so we can dequeue to sort that specific digit.
We sort from the back all the way to the front digit by digit.
Each time we enqueue/dequue the entire list time is O(N) and since we must do the same
operation k times, k being the length of the longest number the time complexity for
radix sort is always O(NK) no matter what the condtion is.


### Time Complexity
**Worse**: O(NK)
**Best**: O(NK)

** More Coming.... **