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

## Post Model

```
rails g model Post title:string content:text
```

- This creates a first migration

To run a migration

```
rails db:migrate
```
