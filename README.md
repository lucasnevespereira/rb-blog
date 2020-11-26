# Rb-Blog app

Create new rails app
`rails new rb-blog`

Install dependencies
`bundle`

Serve the application
`rails s`

## Installation dependecies

Install other gems (dependencies) to make our life easier :)

Go to Gemfile and add
`gem "bulma-rails", "~> 0.9.1"`
`gem 'simple_form'`

Run `bundle` again to install new dependencies

Generate Form Generator
`rails generate simple_form:install`

For Bulma CSS go to `assets/stylesheets/application.scss` and add

`@import "bulma";`

In `Gemfile` -> group development add:

```
gem "better_errors"
gem "binding_of_caller"
gem ‘guard-livereload’, ‘~> 2.5’, require: false
```

Run `bundle`

Run `guard init livereload`

Start guard it will be waiting for changements for live reload like nodemon
Run `bundle exec guard` in another terminal window

## Posts Controller

`rails g controller posts`

In `posts_controller.rb` add an index method

```
class PostsController < ApplicationController
  def index
  end
end
```

In `app/views/posts` create a `index.html.erb` and add a simple h1 tag

```
<h1 class="title">Blog Index</h1>
```

## Setup Posts Route

In `config/routes.db` add

```
  resources :posts
```

<b>Additional:</b> If you want main route to redirect to posts page add under `resources :posts` :

```
 root "posts#index"
```

To see all routes and Controllers Actions on routes

```
rake routes
```

Example of rake routes result for posts

```
Prefix  Verb   URI Pattern                                 Controller#Action
posts     GET    /posts(.:format)                           posts#index
          POST   /posts(.:format)                           posts#create
new_post  GET    /posts/new(.:format)                       posts#new
edit_post GET    /posts/:id/edit(.:format)                  posts#edit
post      GET    /posts/:id(.:format)                       posts#show
          PATCH  /posts/:id(.:format)                       posts#update
          PUT    /posts/:id(.:format)                       posts#update
          DELETE /posts/:id(.:format)                       posts#destroy
root      GET    /                                          posts#index
```

## Post Model

```
rails g model Post title:string content:text
```

- This creates a first migration

To run a migration

```
rails db:migrate
```

## Create new post method

In `posts_controller.rb` add

```
  def new
    @post = Post.new
  end

  def create
    @post = Post.new(post_params)

    if @post.save
      redirect_to @post
    else
      render 'new'
    end
  end

  private

  def post_params
    params.require(:post).permit(:title, :content)
  end
```

Add a template `new.html.erb` for `Post.new`
Create a simple form (using simple_form gem here)

```

<div class="section">
  <%= simple_form_for @post do |f| %>
    <div class="field">
      <div class="control">
      <%= f.input :title, input_html: {class: 'input'}, wrapper: false, label_html: {class: 'label'} %>
      </div>
    </div>
    <div class="field">
      <div class="control">
      <%= f.input :content, input_html: {class: 'textarea'}, wrapper: false, label_html: {class: 'label'} %>
      </div>
    </div>
    <%= f.button :submit, 'Create new post', class: "button is-primary"%>
  <% end %>
</div>

```

## Create a show Post method

Still in `posts_controller.rb` add a show method that will find our created posts

```
  def show
    @post = Post.find(params[:id])
  end
```

Add a template `show.html.erb` for show method

```
<div class="section">
  <div class="container">
    <h2 class="title"> <%= @post.title %> </h2>
    <div class="content">
        <%= @post.content %>
    </div>
  </div>
</div>
```

## Show all posts

In `posts_controller.rb` create a new variable `@posts` in the `index` method that will find all posts

```
  def index
    @posts = Post.all.order("created_at DESC")
  end
```

Then display them in the `index.html.erb` template

```

<section class="section">
  <div class="container">
    <% @posts.each do |post| %>
      <div class="card">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4"> <%= post.title %></p>
            </div>
          </div>
          <div class="content">
            <%= post.content %>
          </div>
        </div>
      </div>
    <% end %>
  </div>
</section>
```
