---
layout: post
title:  "Implementing editable text with Angular-xeditable"
date:   2016-12-26 21:18:39 +0000
---


Recently I was building a small MVC CRUD To-do application with Ruby on Rails and Angular front-end. I really wanted to implement editable text so the user can simply click on the text, edit it, and save it without having to go to a separate route to edit a simple todo. I was able to come up with a way to edit the text by simple doing a ng-show and a ng-hide. Basically I would have a to-do in an <h3> tag, once a user clicked on this tag the <h3> would hide and an input field would show allowing you to edit the text. This fix ended up working for me but it was extremely clunky and simply ugly having to css the crap out of the input field to make it look relatively decent.

**Angular-xeditable to the rescue**

Angular-xeditable is a library directives that allows you to create editable elements. I simply included the CDN in my application then added "xeditable" to my dependencies and it was ready to go! In my html I simply added the following code :

`      <a blur="submit"   href="#" editable-text="list.name">{{ list.name || 'empty' }}</a>`

You add editable-text directive with what you want to be editable which in this case I wanted my list.name to be editable and BAM! Everything looks great right out of the box!
