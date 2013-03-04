---
layout: post
title: "Fixing Random Rails Attribute Exceptions"
date: 2013-03-04 11:02
comments: true
external-url: 
categories: Rails
---

In the previous weeks I found in my Rails log that there were random exceptions when I was trying to access some attributes from current_user, like `current_user.id`, and I was pretty sure that user had logged in when accessing such attributes.

All the exceptions were quite random. The statements which cased these exceptions worked for the most time. Here are some exception traces:

```

NoMethodError (undefined method `to_sym' for nil:NilClass):
  activerecord (3.2.11) lib/active_record/sanitization.rb:60:in `block in expand_hash_conditions_for_aggregates'
  activerecord (3.2.11) lib/active_record/sanitization.rb:59:in `each'
  activerecord (3.2.11) lib/active_record/sanitization.rb:59:in `expand_hash_conditions_for_aggregates'
  activerecord (3.2.11) lib/active_record/relation/query_methods.rb:326:in `build_where'
  activerecord (3.2.11) lib/active_record/relation/query_methods.rb:136:in `where'
  activerecord (3.2.11) lib/active_record/querying.rb:9:in `where'
  orm_adapter (0.4.0) lib/orm_adapter/adapters/active_record.rb:17:in `get'
  devise (2.1.2) lib/devise/models/authenticatable.rb:183:in `serialize_from_session'
  devise (2.1.2) lib/devise/rails/warden_compat.rb:29:in `deserialize'
  warden (1.2.1) lib/warden/session_serializer.rb:35:in `fetch'
  warden (1.2.1) lib/warden/proxy.rb:212:in `user'
  warden (1.2.1) lib/warden/proxy.rb:318:in `_perform_authentication'
  warden (1.2.1) lib/warden/proxy.rb:127:in `authenticate!'
  devise (2.1.2) lib/devise/controllers/helpers.rb:48:in `authenticate_user!'
  activesupport (3.2.11) lib/active_support/callbacks.rb:451:in `_run__2120724129680932349__process_action__409155903620940597__callbacks'
  activesupport (3.2.11) lib/active_support/callbacks.rb:405:in `__run_callback'
  activesupport (3.2.11) lib/active_support/callbacks.rb:385:in `_run_process_action_callbacks'
  activesupport (3.2.11) lib/active_support/callbacks.rb:81:in `run_callbacks'
  actionpack (3.2.11) lib/abstract_controller/callbacks.rb:17:in `process_action'
  actionpack (3.2.11) lib/action_controller/metal/rescue.rb:29:in `process_action'
  actionpack (3.2.11) lib/action_controller/metal/instrumentation.rb:30:in `block in process_action'
  activesupport (3.2.11) lib/active_support/notifications.rb:123:in `block in instrument'
  activesupport (3.2.11) lib/active_support/notifications/instrumenter.rb:20:in `instrument'
  activesupport (3.2.11) lib/active_support/notifications.rb:123:in `instrument'
  actionpack (3.2.11) lib/action_controller/metal/instrumentation.rb:29:in `process_action'
  actionpack (3.2.11) lib/action_controller/metal/params_wrapper.rb:207:in `process_action'
  activerecord (3.2.11) lib/active_record/railties/controller_runtime.rb:18:in `process_action'
  ……
```

```
ActiveRecord::UnknownPrimaryKey (Unknown primary key for table users in model User.):
  app/concerns/xxx.rb:15:in `xxxxxx'
  app/controllers/items_controller.rb:37:in `xxxxxx'
```

The Rails application is running on Debian 6.0.2 x86_64, powered by unicorn 4.1.1, MySQL 5.1 and nginx 1.0.12.

At first I thought the problem was related with old version of [devise](https://github.com/plataformatec/devise), but after upgrading it to the latest stable version, the problem still existed. And I also tried several other approaches, but none of them worked.

One day I found in the log that occasionally it took a SQL SELECT statement 800ms to get result from a table with less than  100 entries. Then I realised MySQL was overloaded.

My previous configuration of unicorn and database created 8 unicorn worker processes, each maintaining 5 concurrent connections (5 is the default value) to MySQL, which means there were 40 concurrent connections to MySQL. I changed it to 4 processes, each with 2 MySQL connections. Since that similar exceptions have never occurred in the last week.

This is my tedious log of how this bug is fixed. Hope it can help you.
