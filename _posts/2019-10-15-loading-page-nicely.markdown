---
layout: post
title:  "Loading pages nicely (aka defer vs. DOMContentLoaded)"
date:   2019-10-15 08:00:00 -0400
categories: javascript best practice
---

While doing my JS labs, I encountered lots of null values while trying to learn about event listeners or how to 
extract valuable information out of an existing HTML element. So, what went wrong and what I should've been doing? 

First, let's go through the process of an HTML page once it reaches the browser. Remember, 
HTML is no different than a piece of non-meaningful text if there is nothing which knows how to understand (parse) it. 
For that, we have our browser. The DOM (Document Object Model) constructed at the time of page load. While going line 
by line, the browser will capture different HTML elements and will build the DOM out of it. The DOM is a hierarchical 
representation of the elements which we then can access through our javascript scripts.
When the browser loads HTML and comes across a `<script>...</script>` tag, it can’t continue building the DOM. 
It must execute the script right away. The same happens for external scripts `<script src="..."></script>`: 
the browser must wait until the scripts downloaded, execute it, and only then process the rest of the page. 

One good practice is to declare our javascript right before the and of the page before the body element is 
being closed `</body>`. On the opposite side, it is advisable to declare our stylesheets right at the `<head>` element. 
Declaring our scripts as part of the `<head>` element may lead to an unexpected behavior. 
You might wonder why is it a problem, let's assume you have a js page with lots of declarations, and functionalities.
JS will run first and will try to find elements from our HTML world, but WAIT! We have a problem! 
the tags and the information they carry are not loaded yet, and our script can't find them and cant modify them.

```html
<body>
  ...all content is above the script...

  <script src="someJS.js"></script>
</body>
```

The browser notices the script (and can start downloading it) only after it parsed the full HTML document 
and represents it as the DOM. For heavy HTML documents, that may be a noticeable delay.

We can also leave it at the top of the page and ask defer to help us out.
The defer attribute tells the browser to execute the script file once the HTML document parsed.
Here is an example where would you like to locate the attribute.
```
<script defer src="script.js"></script>
```

Another solution we have for this issue is an event listener on the document that will say 
"fire up everything as soon as this page content loads. and DOM is fully constructed".

For more info please check out: [https://javascript.info/script-async-defer](https://javascript.info/script-async-defer)