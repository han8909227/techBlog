---
layout: blog
title: Reverse Polish Notation
date: 2018-02-18 16:41:56
tags:
- interview
- reverse polish notation
- arithmetic expression
categories:
- leetcode
---

# Leetcode 150 Reverse Polish Notation
## Original Problem

{% codeblock lang:python %}

# Evaluate the value of an arithmetic expression in Reverse Polish Notation.

# Valid operators are +, -, *, /. Each operand may be an integer or another expression.

# Some examples:
#   ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
#   ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6

{% endcodeblock %}

<!--more-->

## Approach
In everday life we evaluate numbers with operators in the form of `a + b` this is called infix notatio, meaning the operator is in between the two values being operated on.
Polish notaiton, also known as prefix notation has operator in front of the operands in the form of `+ a b`.
You might've guessed it! Reversed-polish-notation, also called postfix notation has the operands before the operator `a b +`, this problem is asking us to write a function that would take in an array of post-fix operations and return the end value.
To solve this problem there are recursive strategies we can use, but it is most famous for the stack approach.
Start with a stack, append the two operands into the stack, use the operator to operate on the two operands(vals) and append the result back to the stack. (this way we always have the current val in the operation to work with).
In the end all the operands in the stack should be reduced to a single value via all the operators throughout the process.


## Implementation

{% codeblock lang:python %}

import operator


def rpn(tokens):
    """."""
    stack = []
    op = '+-*/'
    operation = {
        '+': operator.add,
        '-': operator.sub,
        '*': operator.mul,
        '/': operator.floordiv  # same as // in python
    }

    for num in tokens:
        if num not in op:
            stack.append(int(num))
        else:
            val_1 = stack.pop()
            val_2 = stack.pop()
            re = operation[num](val_2, val_1)
            stack.append(re)
    return stack.pop()


if __name__ == '__main__':
    a = ["2", "1", "+", "3", "*"]
    b = ["4", "13", "5", "/", "+"]
    print('RPN for ' + str(a) + ' is ' + str(rpn(a)))
    print('RPN for ' + str(b) + ' is ' + str(rpn(b)))

 {% endcodeblock %}


https://leetcode.com/problems/evaluate-reverse-polish-notation/
