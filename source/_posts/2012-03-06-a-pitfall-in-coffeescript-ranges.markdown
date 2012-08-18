---
layout: post
title: "A Pitfall in CoffeeScript Ranges"
date: 2012-03-06 15:38
comments: true
categories: [CoffeeScript]
---

Ranges in CoffeeScript look similar to Ruby ranges, except for one big divergence. When used in a reversed order, ranges in CoffeeScript will return an array of revered items, while in Ruby an empty sequence will be generated:

{% codeblock %}
# Ruby
(2..0).to_a  # []

# CoffeeScript
[2..0] # [2, 1, 0]
{% endcodeblock %}

I am not sure why it is designed in this way. Just be careful of this pitfall when dealing with ranges in CoffeeScript.
