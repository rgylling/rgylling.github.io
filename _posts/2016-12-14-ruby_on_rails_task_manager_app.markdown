---
layout: post
title:  "Ruby on Rails Task Manager App"
date:   2016-12-14 22:40:12 +0000
---


For the Ruby on Rails project I thought a simple task management application would be a good choice to display a good CRUD application. The application is similar to my Sinatra to-do list application with more of the robust magic that rails provides me. Also allowing the Devise gem to lend me some magic when it came down to the user authentication side of things.

**The challenge**

I think the most challenging part of building this application was getting Devise to work with how I wanted to route the user around my application. I thought having a user going to multiple routes for logging in or signing up was lacking on the user experience side of things. Since I wanted users to be greeted with a login form and/or sign up form as soon as they got to the root route of my application I had to devise (see what I did there) a way to use the Devise gem to display the log in/sign up views in the root view of my application.

**The solution**

My solution to implementing the log in and sign up into the root of my application was converting the devise views into partials so I can access them anywhere in my application. After making the log in and sign in partials I used bootstraps togglable tabs to allow the user to tab between the log in form and/or the sign up form.
