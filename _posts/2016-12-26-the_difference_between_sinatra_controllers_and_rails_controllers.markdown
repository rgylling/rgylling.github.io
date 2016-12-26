---
layout: post
title:  "The difference between Sinatra controllers and Rails controllers"
date:   2016-12-26 21:06:15 +0000
---


Switching from Sinatra to Rails was a little confusing to me at first looking at the way each framework layed out their file structure. With Sinatra your controllers basically hold all of your code used for routing and handing off information. A example of what a basic controller in Sinatra looks like :

```
class TodosController < ApplicationController 
	get '/todos/:id' do
    if logged_in?
      @todo = Todo.find_by_id(params[:id])
      erb :'todos/show_todo'
    else
      redirect to '/login'
    end
  end
end
```


As you can see the routing is included with the controller with the get 'route' do piece of code. This is all good until you switch over to Rails and see how the frameworks file structure is layed out. With Rails the controllers have no routing what so ever. Routing is separated from the controller and now lives in its own file in the config folder (routes.rb). Without routes included in the controller a typical controller looks like :

```
class ListsController < ApplicationController

  def index
    @lists = current_user.lists.all
  end

end
```
