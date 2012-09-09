---
layout: post
title: "Useful Methods in Kaminari"
date: 2012-09-09 23:18
comments: true
categories: [Rails]
published: true
---

The famous Rails paginator
[Kaminari](https://github.com/amatsuda/kaminari/) provides some
methods in query objects, which may be useful for customizing
views. They are not listed on the document, you may find them in
[lib/kaminari/models/page_scope_methods.rb](https://github.com/amatsuda/kaminari/blob/master/lib/kaminari/models/page_scope_methods.rb):

- total_pages (alias num_pages)
- current_page
- first_page?
- last_page?

Method names are intuitive enough to show what the method returns.
