---
layout: post
title: "Multiple Feeds for Octopress"
date: 2013-01-01 17:43
comments: true
external-url: 
categories: Octopress
---

Before writing in Octopress, I was using Wordpress as blog platform. Wordpress provides Atom seed via /feed/, and after switching my blog platform to Octopress (the blog url is not changed), Atom seed is published through /atom.xml, which means subscribers to my Wordpress will not notified for future blog updates.

I figured out two approaches to make them happy. One way is to redirect /feed/ requests to /atom.xml. Take nginx as an example, add the following lines to the site configuration:

```
location = /feed/ {
    rewrite ^(.*)$ http://blog.yxwang.me/atom.xml;
}
```

Meanwhile if [.htaccess](http://httpd.apache.org/docs/2.2/howto/htaccess.html) is supported on your server you can also define redirection with it.

Recently I switched to another static web service, neither .htaccess nor nginx configuration is allowed. I have to find new way to make /feed/ provides Atom. Here is one simple way to do it, by adding two lines to the end of :generate task, the script will save a clone of atom.xml to /feed/index.html:

``` ruby
desc "Generate jekyll site"
task :generate do
  raise "### You haven't set anything up yet. First run `rake install` to set up an Octopress theme." unless File.directory?(source_dir)
  puts "## Generating Site with Jekyll"
  system "compass compile --css-dir #{source_dir}/stylesheets"
  Rake::Task['minify_and_combine'].execute
  system "jekyll"
  system "mkdir -p #{public_dir}/feed"
  system "cp #{public_dir}/atom.xml #{public_dir}/feed/index.html"
end
```

Now I can see my latest blog posts with old /feed/ url (Note that the blog mentioned here is [another one](http://blog.yxwang.me/)) written in Chinese. Hope this trick can help you as well.
