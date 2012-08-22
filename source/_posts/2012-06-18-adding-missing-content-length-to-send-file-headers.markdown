---
layout: post
title: "Adding Content-Length to send_file Headers"
date: 2012-06-18 19:52
comments: true
categories: [Rails]
---

Some clients and networking libraries may expect 'Content-Length' in response headers when downloading files. However, this parameter is not provided in Rails send_file method. To add content size to the header, you may just add a line next to the send_file method:

{% codeblock lang:ruby %}
def download
    filename = params[:name]
    send_file(filename)
    headers['Content-Length'] = File.size(filename)
end
{% endcodeblock %}
