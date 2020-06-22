---
layout: post
title:      "Selection Sort"
date:       2020-06-22 02:41:01 +0000
permalink:  selection_sort
---


The Selection sort algorithm works by iterating through an unsorted list, finding the smallest element and placing it at the beginning of the list. Then, the next smallest element is placed behind the first element; this continues until all elements in the list are sorted. 

Due to the nested loops in this algorithm, it is not very efficient. It has a time complexity of O(n^2), however, it does have a space complexity of O(1).

Below is an implementation of the selection sort in JavaScript:

```
function selectionSort(array) {
    for (let i = 0; i < array.length; 1++) {
         let smallest = i
         let new = array[i]
        for(let j = i +1; j < array.length; j++) {
	         if(array[j] < array[smallest]) {
		       smallest = j
	         }
        }
       array[i] = array[smallest] 
       array[smallest] = new
    }
   return array
}

selectionSort([5,4,3,73,1,61])


=> [1, 3, 4, 5, 61, 73]
```
