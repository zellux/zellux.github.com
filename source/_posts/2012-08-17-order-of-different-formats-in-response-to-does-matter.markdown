---
layout: post
title: "Order of different formats in response_to does matter"
date: 2012-08-17 19:48
comments: true
categories: [Rails]
---

For example, the following code snippet works well for most browsers:

{% codeblock lang:ruby %}
respond_to do |format|
  format.json { blah blah }
  format.html
end
{% endcodeblock %}

But some browsers, especially embedded webkit components, may set ContentType to `*/*` in request headers. In this case, they will get JSON data instead of HTML if they do not explicitly specify .html format.

So as long as it is not intended, put format.html before format.json will always be a better choice.
