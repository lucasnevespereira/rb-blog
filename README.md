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

`gem 'simple_form'`

Run `bundle` again to install new dependencies

Generate Form Generator
`rails generate simple_form:install`

In `Gemfile` -> group development add:

`gem ‘guard-livereload’, ‘~> 2.5’, require: false`

Run `bundle`

Run `guard init livereload`

Start guard it will be waiting for changements for live reload like nodemon
Run `bundle exec guard` in another terminal window

## First Controller

`rails g controller posts`
