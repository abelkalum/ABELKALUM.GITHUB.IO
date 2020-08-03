---
layout: post
title:      "Sinatra CRUD App"
date:       2020-08-02 19:54:00 -0400
permalink:  sinatra_crud_app
---

It has been an interesting few weeks building a Sinatra app that allows the user to create, read, update, and delete information. In this project, I was also required to ensure that the Sinatra web application I build has an app directory that utilizes MVC (Models, Views, and Controllers) paradigm. Essentially, the MVC directories have the following unique functions:
Models: represents the data and object logic of our application. This is where you define the attributes of each class.
Views: represents the front-end of the app. The user interacts with this part directly. It generally consists of HTML, CSS,  and JS.
Controllers: represents the application logic, which is the interface and flow of the application. This is where application configurations, routes, and controller actions are implemented.
As you can see each directory deals with a separate function/concern but all work together to run the app from front-end (views) to the back-end (models). The controllers relay data between the web browser and the app.
My main controller was the application_controller and it inherited powerful capabilities from Sinatra::Base which provides the context for all evaluation in a Sinatra application. The other two controllers were users_controller and diary_entries controller. These two controllers inherited the defaults and behaviors defined in the application_controller. These inherited defaults and behaviors included application_controller’s authentication methods (ex. current_user and logged_in?) and authorization methods (ex. authorized_to_edit?(diary_entry)).
In my Models, the user has_many :diary_entries and has_secure_password besides validating the presence of the name and email of the user. On the other hand, the diary entry belongs to the user. To automatically add date and time to the user’s entries, I employed the method below within the Models directory:
```
def formatted_created_at 
    self.created_at.strftime("%A, %d %b %Y %l:%M %p")
 end
```
Below are the format directives for the above method:

%A - The full weekday name (``Sunday'')

%d - Day of the month, zero-padded (01..31)

%b - The abbreviated month name (``Jan'')

%Y - Year with century (can be negative, 4 digits at least)

%l - Hour of the day, 12-hour clock, blank-padded ( 1..12)

%M - Minute of the hour (00..59)

%p - Meridian indicator, uppercase (``AM'' or ``PM'')

One of my entries, therefore, looked like this:
```

   <b> Sinatra::Base </b>

   Today I learned that Sinatra::Base class provides the context for all evaluation in a Sinatra application.

   Created by: Foxy

   Created on Sunday, 02 Aug 2020 8:12 PM

   <a href="#">Edit</a>

   <a href="#">Delete this Entry</a> 

   <a href="#">Back</a> 
```
The user has the option of editing, deleting, or going back to their show page to create a new entry, see all other entries, or log out.
