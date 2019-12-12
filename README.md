[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Rails API Single Resource

## Objectives

By the end of this lesson, developers should be able to:

-   Follow along in the creation of an API.
-   Build a complete server side API in Rails
-   Create a model with full CRUD capability

## Preparation

1.  Rails installation completed

## Useful Documentation

-   [`active_model_serializers`](https://github.com/rails-api/active_model_serializers)
-   [`ruby`](https://www.ruby-lang.org/en/)
-   [`postgres`](http://www.postgresql.org)

This is intended for developers to follow along as I build a library API. You
may follow along as I code but I will not slow down or share this code. Later
in this training we will have a code along.

## Methodical, Error-Driven Development

Status checks will be frequent. As developers we want to be meticulous and make
sure we're getting errors where expected as we build our API.

This is called "error-driven development". The goal is to see an error, and to
learn what error to expect. Embrace the errors, and they will tell you what
your next task is.

We'll trigger errors by issuing `curl` requests.

## Routing

We're making a library API Right? Let's try checking to see if there are any
books by navigating to `localhost:3000/books`

You should get an error similar to the following:

```bash
Routing Error
No route matches [GET] "/books"
```

Whoops! We haven't made any routes yet!

As you learned in the previous lesson, a route indicates which controller
action will be triggered when a particular type of HTTP request arrives at a
given URL.

In order for our API to respond to GET requests at the `/books` URL, we'll need
to create a Route that specifies what to do when that type of request comes in.

Add the following code to `config/routes.rb`:

Long-hand (used for custom routes)
```ruby
get '/books', to: 'books#index'
```

Short-hand
```ruby
resources :books, only: [:index]
```

This tells Rails, "When you receive a GET request at the URL path `/books`,
invoke the `index` method specified in the BooksController class."

We changed a small bit of code, let's see if anything has changed.

It looks like our error has changed to:

```ruby
>> uninitialized constant BooksController
```

## Controller

We haven't _defined_ a BooksController class yet, so if we try to access
`localhost:3000/books`, we'll get another error:

The purpose of a controller is to handle requests of some particular type. In
this case, we want to create a new controller called `BooksController` for
responding to requests about a resource called 'Books'.

Rails has a number of generator tools for creating boilerplate files very
quickly. To spin up a new controller, we can just run `bin/rails generate
controller books`.

This will automatically create a new file in `app/controllers` called
`books_controller.rb`, with the following content:

```ruby
class BooksController < ApplicationController
end
```

Not all controllers handle CRUD,
but those that do tend to follow the following convention for their routes
and controller actions:

| Action  | What It Does                             | HTTP Verb | URL           |
|:-------:|:----------------------------------------:|:---------:|:-------------:|
| index   | Return a list of all resource instances. | GET       | `/books`     |
| create  | Create a new instance of a resource.     | POST      | `/books`     |
| show    | Return a single instance of a resource.  | GET       | `/books/:id` |
| update  | Update a single instance of a resource.  | PATCH     | `/books/:id` |
| destroy | Destroy a single instance of a resource. | DELETE    | `/books/:id` |

Let's add an `index` method to `BooksController`.

```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all

    render json: @books
  end
end
```

Let's make a request and see if our error message has changed.

It seems we have an `uninitialized constant`! This is because we have yet to
tell rails what a `book` is, it doesn't know how to **model** the data.

## Model

Let's generate a model by entering `bin/rails generate model Book title:string
author:string`

Never blindly accept generated code. Always inspect it.

Let's check out server and see if our error message has changed.

It seems we have to migrate, let's do that.

## Migrations

Run `bin/rake db:migrate` in the root of this books directory.

Let's see if our error has changed.

We can see what appears to be JSON, but there are no books! That's because we
have not added any.

## Rails Console

First let's enter our `rails console` so we can make use of our models. This
lets us interact with Rails from the command line.

We're going to create a single book:

### CRUD: C

```ruby
Book.create([{ title: 'Less Funny Than Jason', author: 'Lauren Fazah'}])
```

We can even use other methods such as `.new` and `.save`.

Now navigate to `localhost:3000/books` and see if anything has changed.

### CRUD: R

If want to use Active Record for seeing what is in our data store we can do so
by looking for a speific field.

```ruby
Book.find_by(author: 'Lauren Fazah')
# returns the first author

Book.where(author: 'Lauren Fazah')
# returns all results where author == 'Lauren Fazah'

Book.last
# returns the last book in the collection
```

There are more ways to read and organize the data using Active Record. I would
encourge you to look up more in your off time.

### CRUD: U

Let's update one of our books using Active record

```ruby
book = Book.find_by(title: 'Less Funny Than Jason')
book.update(title: 'Less overall cool factor than Jason: The Sequel')

# You could also string this together
Book.find_by(title: 'Less overall cool factor than Jason: The Sequel').update(title: 'JASON IS AWESOME THE TRILOGY')
```

Now navigate to `localhost:3000/books` and see if anything has changed.

### CRUD: D

Finally, if we want to remove a book with Active Record we simply do:

```ruby
Book.find_by(author: 'Jason Weeks').destroy
```

Note: `find_by` will only destroy *one* book. If we want to destroy *all* the
books by Jason, we have to use `where`.

Now navigate to `localhost:3000/books` and see if anything has changed.


Follow the steps outlined in good Error Driven Development

1. Route
    - Test the route, see that a route does not exist
    - Add the route
    - Test the route, see that a route does exist
1. Controller
    - Test the route, see that a route does exist but controller does not
    - Add the controller
    - Test the route, see that a controller exists
1. Model
    - Test the route, see that a controller exists but model does not
    - Add the model
    - Test the route, see that a Model exists
1. Migrations
    - Test the route, see that a Model exists but migrations must be run
    - Run migrations
1. View
    - Test the view, see that it does not exist
    - Add the view
1. Test Feature
    - Test the route, ensure actions are successful
    - Use Rails Console to ensure all data persists as expected

Let's load example data by running `bin/rake db:examples`. It's a good idea to
write example data so you can test your own APIs.

## Tips

-  Be meticulous, did you check your pluralization? is your spelling correct?
   Did you miss and `end`?
-  Test frequently, check for errors in your browser and server.
-  Follow your errors, they typically give you a line number, be patient.  You
   should be able to identity the exact line of your bug before you ask for
   assistance.
-  Remember to use the generators to your advantage. They can save you valuable
   time.

## Tasks

Developers should run these often!

-   `bin/rake routes` lists the endpoints available in your API.
-   `bin/rake test` runs automated tests.
-   `bin/rails console` opens a REPL that pre-loads the API.
-   `bin/rails db` opens your database client and loads the correct database.
-   `bin/rails server` starts the API.
-   `scripts/*.sh` run various `curl` commands to test the API. See below.

<!-- TODO -   `rake nag` checks your code style. -->
<!-- TODO -   `rake lint` checks your code for syntax errors. -->

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
