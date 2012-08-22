---
layout: post
title: "Order of Formats in response_to Does Matter"
date: 2012-08-17 19:48
comments: true
categories: [Rails]
---

The following code snippet works well for most browsers:

{% codeblock lang:ruby %}
respond_to do |format|
  format.json { blah blah }
  format.html
end
{% endcodeblock %}

But some browsers, especially embedded webkit components, may set ContentType to `*/*` in request headers. In this case, they will get JSON data instead of HTML if they do not explicitly specify .html format in URL.

So as long as it is not intended, putting format.html before format.json will always be a better choice.
