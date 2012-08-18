---
layout: post
title: "Optimizing Page Rendering Speed for iPad 3"
date: 2012-03-27 18:16
comments: true
categories: [WebDev]
---

When developing online book store in [Tangcha](http://tangcha.tc), we were confronted with slow web page rendering issue on iPad 3, and finally found out two optimizations to make it much faster. The approaches were also posted on [Stack Overflow](http://stackoverflow.com/a/10721238/111896).

1. Avoid using CSS3 effects. We used a lot of CSS3 shadows in previous versions, which slowed down rendering process on iPad 3 a lot. After replacing those shadow effects with background images, performance got greatly improved on iPad 3.

2. Optimize Javascript. Our application has some scrollable components, whenever user scrolls the component some Javascript code will be executed to do some loading work, like loading images in a lazy way. On iPad 3 scrolling will delay for 500ms when user tries to scroll from one page to the next. Then we found some unnecessary image loading work were performed in the scrolling callback, after removing them, the scrolling performance is acceptable.
