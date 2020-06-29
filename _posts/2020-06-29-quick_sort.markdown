---
layout: post
title:      "Quick Sort"
date:       2020-06-29 06:22:23 +0000
permalink:  quick_sort
---


The Quick sort algorithm is a divide and conquer algorithm, meaning it breaks itself down into smaller and smaller bits. It works by choosing a pivot point and then splitting the list into two parts. Sorting the elements by putting the elements before the pivot if it is smaller and putting the elements larger than the pivot after it.

Quick sort has a worst case time complexity of O(n^2), this occurs if the pivot happens to be on either end of the spectrum. If it is not, the time complexity is the same as the space complexity,  O(n log(n)).


Below is an implementation of the selection sort in JavaScript:

