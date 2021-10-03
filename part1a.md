# Part 1a - Scaffolding with Rails 

Beginners introduction to scaffolding with Ruby on Rails. 


## Generate the scaffold

1. Generate the scaffold for the `Projects` model, view, controller. 

```ruby

rails generate scaffold Projects title:string description:text

```
<details>
  <summary><strong>Self Check Question:</strong> What is scaffolding?</summary>
  <p><blockquote>Rails scaffolding is a quick way to generate some of the major pieces of an application. If you want to create the models, views, and controllers for a new resource in a single operation, scaffolding is the tool for the job. <a href="https://guides.rubyonrails.org/v3.2/getting_started.html#getting-up-and-running-quickly-with-scaffolding
" target="_blank">Read More</a></blockquote></p>
</details>

2. Migrate the database: 
```ruby
rake db:migrate
```

<details>
  <summary><strong>Self Check Question:</strong> How does Rails decide where and how to create the development database?  (Hint: check the <code>db</code> and <code>config</code> subdirectories)</summary>
  <p><blockquote>The <code>rake db:migrate</code> command creates a local development database (following the specifications in <code>config/database.yml</code>) and runs the migrations in <code>db/migrate</code> to create the app's schema.  It also creates/updates the file <code>db/schema.rb</code> to reflect the latest database schema.  <strong>Note: it's important to keep this file under version control.</strong> </blockquote></p>
</details>
<br />

<details>
  <summary><strong>Self Check Question:</strong> What tables got created by the migrations?</summary>
  <p><blockquote>The <code>project</code> table itself and the rails-internal <code>schema_migrations</code> table that records which migrations have been run.</blockquote></p>
</details>

3. Run the server
```ruby

rails s -b 0.0.0.0

```

4. Naviage to `localhost:3000/projects` and ensure that you can run CRUD operations for the projects

5. Add `root` to `config/routes.rb`:

```ruby

Rails.application.routes.draw do
  root "projects#index"
  resources :projects
end

```
<details>
  <summary><strong>Self Check Question:</strong> Why did we have to add a root route?</summary>
  <p><blockquote>You can specify what Rails should route '/' to with the root method</blockquote></p>
</details>

6. Naviage to `localhost:3000/` and ensure that you can still run CRUD operations for the projects

7. Check in your code to GitHub
```bash
$ git add -A
$ git status #Make sure all the new files are tracked AND on stage for being committed!!
$ git commit -m "Added scaffolding"
$ git push
```

## Helpful links:


* https://guides.rubyonrails.org/v3.2/getting_started.html#getting-up-and-running-quickly-with-scaffolding
