---
layout: post
title:      "JavaScript Eventing"
date:       2020-11-08 21:53:11 -0500
permalink:  javascript_eventing
---


In JavaScript, things that happen in the browser are known as "events". JavaScript "listens" for these events and can respond to it with event handling. There are a number of different events, the categories include resource, network, focus, websockets, session history, form, printing, keyoard, clipboard, mouse, and many more. The most common events include:

Keyboard Events: Keydown, keypress, keyup

Mouse Events: click, mousedown, mouseover, select, mouseleave, scroll

To set up event handling, we add a listener for the specific event, *addEventListener()* takes two arguments:

1. event name
2. a callback function that handles the event

```
const clicking = document.getElementById('name');
clicking.addEventListener('click', function(event) {
  alert('you clicked me!');
});
```

This code here triggers an alert when to pop up when click in the input area in the browser.
