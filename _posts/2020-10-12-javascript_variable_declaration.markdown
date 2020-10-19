---
layout: post
title:      "JavaScript Variable Declaration"
date:       2020-10-12 02:36:51 -0400
permalink:  javascript_variable_declaration
---


Prior to ES6, variables were declared with Var. Since the JavaScript engine works in two phases, first the complilation phase and then the execution phase, depending on where the variable was declared could cause issues with hoisting. Hoisting occurs when a variable can be used before declaring it.  Hoisting applies to variable declarations but not its assignments. Hoisting allows this to work:

```
     function greeting () {
		       return "Hello!";
		 }
		 
		 greeting();
		 
		 // => "Hello!"
		 
	```
	
	the same way as this:
	
	```
	      greeting();
			
			   function greeting () {
		       return "Hello!";
		 }
		 
		  // => "Hello!"
			
	```

To avoid issues with hoisting, variable declarations can be made at the top of its scope. ES6 provided an easier fix for this issue with the new variable declarations *let* and *const*. These two declarations are block scoped and can only be accessed within the block it is defined.
