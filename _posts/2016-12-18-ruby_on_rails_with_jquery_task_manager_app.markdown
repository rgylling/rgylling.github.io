---
layout: post
title:  "Ruby on Rails with JQuery Task Manager App"
date:   2016-12-18 01:21:14 +0000
---


For the Ruby on Rails with JQuery project I enhanced my previous task manager app that was built with just Ruby on Rails. This application is just a beefed up version of my previous task manager app utilizing jquery and ajax to get rid of those pesky page refreshes when requesting information from a database.

**The Challenge**

By far the most challenging aspect of this project was integrating ajax requests with how I previously built the application. For example I have lists and every list has tasks associated, instead of displaying a separate page showing every task I decided to use the lists show page to display every task that is associated with that by looping through the lists tasks and rendering them to the page via ruby. So far this sounds very simple but when adding Jquery to my application what I wanted to do is to add a next button. The next button would display the next list which also displays every task associated with that list without reloading the page. This proposes a challenge as with every task I integrated an edit and delete button via rails button_to helpers which were previously dynamically created while looping through the tasks with ruby. I couldn't just send an ajax request and simply loop through each task associated with that list and append them to the page, I had to also dynamically create the buttons to go along with those tasks.

**The Solution**

I couldn't simple use rails button_to helpers since I was using JQuery and Ajax to request the information, I had to dynamically create the buttons with Javascript which is easier said then done. With every edit and delete button I created with Javascript I also needed to add the lists ID, tasks ID, and also with the delete button I had to create a auth token. I ended up taking all of the created html that rails button_to help provides you and creating it all with a javascript function I created. Here is the code:

```
function deleteButton (listId, taskId, token) {

  var myDeleteButton = "<form class='button_to' method='post' action='/lists/" + listId + "/tasks/" + taskId + "'><input type='hidden' name='_method' value='delete'><input class='button-small btn' type='submit' value='Delete'><input type='hidden' name='authenticity_token' value=" + token + "></form>"

  return myDeleteButton

}
```

As you can see it is pretty messy but it gets the job done. In the function I am passing through the list id, task id, and a auth token that I created. This function creates a delete button much how you would see it formatted through the rails button_to helper. I also had to do something similar for the edit button as well. Now when I receive what I want via the ajax request I just loop through each task and add those dynamically created buttons with every task.

