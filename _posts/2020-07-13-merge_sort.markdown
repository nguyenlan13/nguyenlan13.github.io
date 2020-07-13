---
layout: post
title:      "Merge Sort"
date:       2020-07-13 04:54:32 +0000
permalink:  merge_sort
---


The Merge sort algorithm works by utilizing a divide and conquer approach. The list of elements is divided in half and each subsequent sublist is then divided again. This continues until each list contains just one element. The lists are then put back together by comparing each element and placing the smallest element on front, sorting them. 

This algorithm is fairly efficient, it has a time complexity of O(n log n), however, it does have a space complexity of O(n) because it has to create another variable to hold the additional list .

Below is an implementation of merge sort in JavaScript:

