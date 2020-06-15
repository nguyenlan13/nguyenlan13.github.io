---
layout: post
title:      "Stacks and Queues"
date:       2020-06-15 06:06:58 +0000
permalink:  stacks_and_queues
---


Stacks and queues are higher level, linear data structures that are built using lower level data structures like arrays and linked lists.

A stack, or call stack, operates on the principle of Last In First Out (LIFO). Stacks are unidirectional, meaning it grows in one direction; elements can only be added or removed from the top of the stack. Stacks are usually implemented with a linked list because it is dynamic, but 
it can also be implemented with an array. However, since an array is static, adding more elements than there is space in the array will cause a stack overflow. A web browser and the back button is an example of a stack. The page we are currently viewing is the top of the stack and as we click the back button, it will navigate us to the previous page we were on.

A queue operates on the principle of First in First out (FIFO). Elements are added (enqueue) to the end of a queue and removed (dequeue) from the front of the queue. Similar to a stack, a queue can be implemented by using a linked list or array. Implementing a queue with an array however, will be less efficient because removing an element will require all elements to shift one index over which is a O(n) operation instead of O(1) as seen when using a linked list. An example of a queue is a waiting line at a store checkout, where the first person in line checks out first and then the second person checks out, and so on.


