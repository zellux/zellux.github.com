---
layout: post
title: "Some Notes on RSpec"
date: 2012-05-07 15:40
comments: true
categories: [RSpec, Rails]
---

### Stubbing instance methods

The method `any_instance` allows stubbing instance methods easily. For example, the following line will force calling Item#price to return 10 always:

{% codeblock lang:ruby %}
Item.any_instance.stub(:price).and_return(10)
{% endcodeblock %}

### Stubbing in helper specs

Stubbing in helper specs is similar to stubbing in controller specs. Just remember to add `helper.` before every helper method call.

{% codeblock lang:ruby %}
it 'test current user' do
  helper.stub(:current_user).and_return(user)
  helper.user_avatar.should_not be_empty
end
{% endcodeblock %}

### let and let!
Variables defined by `let` is evaluated in a lazy way. Use `let!` to force the evaluation before each spec.
