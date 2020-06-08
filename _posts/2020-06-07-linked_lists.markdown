---
layout: post
title:      "Linked Lists"
date:       2020-06-07 23:33:04 -0400
permalink:  linked_lists
---


A linked list is a linear and dynamic data structure, meaning there is order like an array but it is dynamic in that its memory allocation is not fixed; it can grow or shrink. Linked lists (singly-linked) consists of a head node that has a pointer that points (reference to) to a series of nodes and ends with a tail node that points to null. A node only contains data and a reference to the next node.

Linked lists can be one solution to collisions in hash tables and also solve the memory allocation issues often seen in arrays. Collisions occur in hashes when two keys occupy the same memory address; linked lists provide a way to resolve this issue by having a given node point to a reference where the next node lives. In arrays, the memory allocation is in a continuous block whereas in linked lists, the memory can be allocated in a scattered manner similarly to a hash. 

