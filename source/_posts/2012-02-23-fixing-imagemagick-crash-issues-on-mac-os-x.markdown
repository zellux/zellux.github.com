---
layout: post
title: "Fixing ImageMagick crash issues on Mac OS X"
date: 2012-02-23 16:04
comments: true
categories: [Libraries, Mac]
---

ImageMagick may be prone to crash on Mac OS X, and it can be avoided by disabling OpenMP when compile the library:

{% codeblock %}
brew install -f imagemagick --disable-openmp
{% endcodeblock %}

