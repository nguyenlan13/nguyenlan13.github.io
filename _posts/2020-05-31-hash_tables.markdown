---
layout: post
title:      "Hash Tables"
date:       2020-06-01 01:33:26 +0000
permalink:  hash_tables
---


Hash tables are a very interesting and useful data structure in that they can provide very fast lookups and insertions. Hash tables can go by different names in different languages. For example, in Ruby it is called a hash and in Javascript it is called an object. 

Hash tables are made up of two parts, an array to hold the data and a hash function that, given a key, determines the index of the array where the data will be stored. The way a hash function works is it takes a given input(key) and it maps it to a memory address. Given a key, it will always output the same value; this function is idempotent. Depending on the situation, this is how we can achieve a time complexity of O(n) (constant time) for lookups and insertions. This does not work in reverse, however. Given the output, we cannot retrieve the input. 

We can think of hash tables as similar to a library, books are the data, shelf is the array, and the Dewey Decimal System is the hash function. The Dewey Decimal System would tell us exactly where to retrieve the book. Although hash tables can greatly optimize our runtime, there is usually a tradeoff with space complexity.
