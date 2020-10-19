---
layout: post
title:      "Lifecycle Methods"
date:       2020-10-18 23:57:21 -0400
permalink:  lifecycle_methods
---


The react component lifecycle consists of three phases, creation (mounting), updating, and deletion(unmounting). To control how a component responds to a change, we can use lifecycle methods.

During the mounting phase, there are two methods available for use: 

*getDerivedStateFromProps* - called right before the render method
*componentDidMount* -  called right after the render method. 

In the updating stage, the available methods are:

*getDerivedStateFromProps* - used in rare situations where state changes are needed before an update
*shouldComponentUpdate* - used right before component re-renders
*getSnapshotBeforeUpdate* - used right before updating
*componentDidUpdate* - invoked right after component updates

Finally, in the deletion or unmounting phase, the available method is *componentWillUnmount*. This method is called right before the component unmounts and it will clear anything that was initially set up in the *componentDidMount* method.


