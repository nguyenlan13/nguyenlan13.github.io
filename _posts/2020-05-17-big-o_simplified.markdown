---
layout: post
title:      "Big-O Simplified"
date:       2020-05-17 19:35:11 +0000
permalink:  big-o_simplified
---


When analyzing the performance of an algorithm, the term big-O notation typically appears. What is big-O?  Big-O is the metric used to describe the efficiency of an algorithm, usually in terms of time(runtime) or space (memory) complexity. It describes the asymptotic upper bound(growth of time or space) of an algorithm as input size grows.

When thinking of time complexity, an everyday analogy could be choosing to wash dishes by hand or by using  a dishwasher(let's say it’s a huge industrial one). If we only had a few dishes, it probably would be faster to wash by hand but as the dishes increased, it could take very long. Meanwhile, if we used the dish washer to wash 1 dish or 100 dishes, it would take the same amount of time. The run time of washing by hand would increase linearly as the number of dishes (input) increases which is denoted as O(n) and using a dishwasher would be constant time, or O(1) because the speed does not depend on the input size. These are just 2 examples of big-O notation but the common notations are (ranked from fastest to slowest) below:


| Notation | Meaning | Usually Indicated By: |
| ---------- | ---------- | ----------------------- |
|    O(1)       |  Constant - Speed is not dependent on input size | No loops |
|O(log n) | Logarithmic - As input doubles, 1 operation is added | Already sorted |
| O(n)  | Linear - Number of operations is proportional to input size | Loops |
| O(n^2) | Quadratic - Number of operations is proportional to input size squared |Nested Loops |


A few simple rules to follow when determining the runtime of a given algorithm is to use the worst case scenario, remove constants and drop nondominant terms.

A runtime can be described using its best-case, average-case, or worst-case scenario but typically the focus is only on the worst-case since it will guarantee that the algorithm will not take any longer. We remove constants and nondominant terms because as input grows, they become insignificant.
For example, if we have O(3n + n^2 + 1000) the constants and lower order terms are removed and we have a runtime of O(n^2), or quadratic time.

In determining space complexity, these rules remain the same but the factors that take up additional memory are variables, function calls, and data structures. There will be times where there are tradeoffs between time and space. If space is more important for a use case, you may opt for an algorithm that saves on space but has a slower runtime and vice versa.

