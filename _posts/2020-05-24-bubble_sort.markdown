---
layout: post
title:      "Bubble Sort"
date:       2020-05-25 00:33:45 +0000
permalink:  bubble_sort
---


Bubble sort has a notorious reputation for being a “bad” sorting algorithm due to its poor performance. An illustration of how this algorithm compares to other sorting algorithms can be seen[ here.](https://www.toptal.com/developers/sorting-algorithms) The bubble sort algorithm iterates through a collection and compares each element one at a time to the element adjacent to it, swapping the elements if it is out of order. This continues until all the elements are sorted. The smallest element “bubbles” towards the front and the largest “bubbles” towards the end.

This algorithm has a time complexity of O(n^2) but a space complexity of O(1). It could be useful if the input size is small or if runtime is not important. An implementation of bubble sort in Ruby is below:

```def bubble_sort(array)
    for i in 0...(array.length - 1) do
        for j in (i + 1)...array.length do
            if array[i] > array[j] 
                array[i], array[j] = array[j], array[i]
            end
        end
    end
    array
end

bubble_sort([6,4,3,78,1,65])


=> [1, 3, 4, 6, 65, 78]
```



