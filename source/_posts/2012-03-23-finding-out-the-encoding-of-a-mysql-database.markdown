---
layout: post
title: "Finding out the encoding of a MySQL Database"
date: 2012-03-23 09:45
comments: true
categories: [WebDev, Database]
---

Find out the encoding of a MySQL database:

{% codeblock %}
SHOW VARIABLES LIKE 'character_set_%';
{% endcodeblock %}

Find out the encoding of a specific table:

{% codeblock %}
SHOW CREATE TABLE table_name;
{% endcodeblock %}
