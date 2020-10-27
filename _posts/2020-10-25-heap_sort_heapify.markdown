---
layout: post
title:      "Heap Sort (Heapify!)"
date:       2020-10-25 21:56:57 -0400
permalink:  heap_sort_heapify
---


A heap sorting algorithm utilizes a binary heap data structure. A binary tree is a data structure that allows each parent node to have a maimum of two children elements, a left and right child. Heaps are binary trees with some additional rules; heaps must follow a specific order where the binary tree is filled up from left to right and it must be a min or max heap. Max heaps require that each parent node is greater or equal to the value of its childen nodes. Given our unsorted array, we transform it into a binary tree. We then swap the largest and smallest node to place the largest number as the root node, this number will be at the end of the array. We then swap each the elements at each node if it is greater than the child element in order to have a max heap again. The largest node will then be the new root node and it would be the next element in the array. This continues until all elements are sorted and the algorithm is complete. This sorting method has a time complexity of O(n log n), or linearthmic time.
