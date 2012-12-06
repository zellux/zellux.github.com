---
layout: post
title: "Traps in Comparing Container Sizes"
date: 2012-12-06 15:28
comments: true
external-url: 
categories: C++
---

I just started learning C++ and occurred a bug related with container size comparison.

The following code looks ok from Java or Ruby's perspective:

``` c
while (front.size() - back.size() > 1) {
    back.insert(*front.rbegin());
    front.erase(--front.end());
}
```

However, there is a critical bug in this code. `size()` method returns a value in `size_type`, which is an unsigned integer. If front.size() is smaller than back.size(), the minus will underflow and result in a very large value, thus making the while loop condition true.

Knowing the reason, it is easy to correct this loop condition as follows:

``` c
while (front.size() > back.size() + 1) {
    back.insert(*front.rbegin());
    front.erase(--front.end());
}
```
