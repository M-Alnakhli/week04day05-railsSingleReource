# Rails Single Resource

Let's build a rails application!

## Objectives

By the end of this, developers should be able to:

- Follow along in the creation of an API.
- Build a complete server side in Rails.
- Create a model with full CRUD capability.

## Code Along: Books

### User Stories

- Version 1:
  - As a user, I want to view a single book
  - As a user, I want to view all books
  - As a user, I want to create a book with a title and author
  - As a user, I want to edit a book's title and author
  - As a user, I want to delete a book

### Entity Relationship Diagram (ERD)

<table>
  <th colspan="2" style="text-align:center">Books</th>
  <tr>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
  </tr>
  <tr>
    <td>author</td>
    <td>string</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

### Methodical, Error-Driven Development

Status checks will be frequent. As developers we want to be meticulous and make
sure we're getting errors where expected as we build our server.

This is called "error-driven development". The goal is to see an error, and to
learn what error to expect. Embrace the errors, and they will tell you what
your next task is.

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

### CRUD for Books

We'll now go through the steps for completing each CRUD action for multiple
resources.

#### Read - index

- `BooksController#index`

#### Read - show

- `BooksController#show`

#### Destroy

- `BooksController#destroy`

#### Update

- `BooksController#update`

#### Create

- `BooksController#create`

## Lab: Create Authors

Let's add an author to our application.

### User Stories
  - As a user, I want to view an author
  - As a user, I want to view all authors
  - As a user, I want to create an author with a given name and family name
  - As a user, I want to edit an author's given name and family name
  - As a user, I want to delete an author

### Entity Relationship Diagram (ERD)

<table style="display:inline">
  <th colspan="2" style="text-align:center">
  Authors
  </th>
  <tr>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>first_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>last_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

Follow the same Error Driven Development steps as you did with books!

### CRUD for Author

#### Read - index

- `AuthorsController#index`

#### Read - show

- `AuthorsController#show`

#### Destroy

- `AuthorsController#destroy`

#### Update

- `AuthorsController#update`

#### Create

- `AuthorsController#create`

## Tasks

Developers should run these often!

- `bin/rake routes` lists the endpoints available in your API.
- `bin/rake test` runs automated tests.
- `bin/rails console` opens a REPL that pre-loads the API.
- `bin/rails db` opens your database client and loads the correct database.
- `bin/rails server` starts the API.

## Additional Resources

- [Rails Docs: Routing](http://guides.rubyonrails.org/routing.html)
- [Rails Docs: Controllers](http://guides.rubyonrails.org/action_controller_overview.html)
- [Rails Docs: Active Record Basics](http://guides.rubyonrails.org/active_record_basics.html)
- [Rails Docs: Active Record Querying](http://guides.rubyonrails.org/active_record_querying.html)
- [Rails Docs: Active Model Basics](http://guides.rubyonrails.org/active_model_basics.html)
- [Rails Docs: Command Line](http://guides.rubyonrails.org/command_line.html)
- [Migration Cheat Sheet](https://www.ralfebert.de/snippets/ruby-rails/models-tables-migrations-cheat-sheet/)
- [Rails Reserved Words](https://reservedwords.herokuapp.com/)
- [Rails Status Symbols](http://www.railsstatuscodes.com/)

