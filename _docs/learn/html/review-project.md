---
title: Review Project
search_title: Review Project HTML
category: learn-html
order: 4
---

Let's explore the project code and write some app code.

## ApplicationController

The starter project comes with an `ApplicationController`. It looks like this:

app/controllers/application_controller.rb

```ruby
class ApplicationController < Jets::Controller::Base
end
```

In general, all of your controllers will inherit from this `ApplicationController`.

## Create Posts Scaffold

Let's create some code for posts resources. We'll generate some starter code again.

    ❯ jets generate scaffold post title:string body:text published:boolean
          invoke  active_record
          create    db/migrate/20231029041209_create_posts.rb
          create    app/models/post.rb
          invoke  resource_route
          route    resources :posts
          invoke  scaffold_controller
          create    app/controllers/posts_controller.rb
          invoke    erb
          create      app/views/posts
          create      app/views/posts/index.html.erb
          create      app/views/posts/edit.html.erb
          create      app/views/posts/show.html.erb
          create      app/views/posts/new.html.erb
          create      app/views/posts/_form.html.erb
          create      app/views/posts/_post.html.erb
          invoke    resource_route
          invoke    helper
          create      app/helpers/posts_helper.rb

The generated code looks something like this:

app/controllers/posts_controller.rb

```ruby
class PostsController < ApplicationController
  before_action :set_post, only: %i[ show edit update destroy ]

  # GET /posts
  def index
    @posts = Post.all
  end

  # GET /posts/1
  def show
  end

  # GET /posts/new
  def new
    @post = Post.new
  end

  # GET /posts/1/edit
  def edit
  end

  # ...
end
```

It's a controller with the basic CRUD methods. Jets will create one lambda function to handle requests for any of the controller methods.

Next, we'll test the app locally.
