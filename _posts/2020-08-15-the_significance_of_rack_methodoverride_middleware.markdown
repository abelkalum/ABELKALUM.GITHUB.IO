---
layout: post
title:      "The Significance of Rack::MethodOverride Middleware"
date:       2020-08-15 20:20:35 +0000
permalink:  the_significance_of_rack_methodoverride_middleware
---


At the end of my Sinatra CRUD app project, I was perplexed why when I tried to delete my entries I could only delete my content but not the title. The delete action was not being completed as the entry still had everything else(title, name of user/creator of entry, date, and time of entry) except for the content of the entry. It didn’t make sense at all. I kept telling myself that a simple fix in the views folder dealing with DELETE action could resolve the issue. After many attempts, I still did not resolve the issue.  Enter Rack::MethodOverride middleware!

Rack::MethodOverride is a very important middleware that enables one to perform controller actions such as PATCH, PUT, or DELETE. It is usually mounted in config.ru just above the controllers. 

My DELETE form in my views looked like this:
```
<form class="" action="/diary_entries/<%= @diary_entry.id %>" method="post">
    <input type="hidden" name="_method" value="DELETE">
    <input type="submit" name="" value="Delete this Entry"> 
</form>
```
It is the hidden input field in the second line of the form above that uses Rack::MethodOverride. It only works if the middleware is mounted above the controllers in config.ru like shown below:

require './config/environment'
if ActiveRecord::Migrator.needs_migration?
  raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end
use Rack::MethodOverride
use UsersController
use DiaryEntriesController
run ApplicationController

The Rack::MethodOverride middleware will interpret any requests with name="method" by translating the request to whatever is set by the value attribute. So in the above example, the post method gets translated to a DELETE request. Without Rack::MethodOverride middleware in your config.ru file your app will not know how to handle patch and delete requests!

