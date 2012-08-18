---
layout: post
title: "Speeding Up String Concatenation in Ruby"
date: 2012-03-30 16:31
comments: true
published: false
categories: [Ruby]
---
When concatenation large chunks of strings in Ruby, operator `<<` will be more efficient than `+`. This is because `+` creates immutable strings and introduces burden on garbage collector, while `<<` mutates the orinal string and thus do not create new objects.

Here is an experiment I made on a machine with 4GB memory and CPU, under Ubuntu 10.10:
