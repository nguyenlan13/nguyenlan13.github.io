---
layout: post
title:      "Destructuring"
date:       2020-09-13 11:04:31 -0400
permalink:  destructuring
---


Destructuring assignment is a javascript expression that helps extract out data from objects and arrays. Destructuring allows us to reduce repetitive code by assigning multiple variables at a time and simplifying the syntax. This can be used with objects or arrays, even their nested structures.

Examples

Object:

```
const object = { first: 'Lan', last: 'Nguyen' };
const {first: f, last: l} = object;
    // f = 'Lan'; l = 'Nguyen'


const {first, last} = object;
    // first = 'Lan'; last = 'Nguyen'
```
		
Array:

```
const numbers = ['one', 'two', 'three'];

const [red, yellow, green] = numbers;
console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"


let hello, bye;

[hello, bye] = [1, 2];
console.log(hello); // 1
console.log(bye); // 2
```
