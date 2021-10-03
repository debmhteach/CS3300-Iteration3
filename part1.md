## Part 1: Preparation: get your app running locally in docker Ubuntu development environment

```sh
$ cd /root/
$ git clone https://github.com/{YOURGITHUBUSERNAME}/{YOURREPONAME}.git # Replace YOURGITHUBUSERNAME with your github username and replace YOURREPONAME with the name of your repo.
$ cd YOURREPONAME
```

After you are in your `YOURREPONAME` directory. Run `rails new .` This command will install a new Ruby on Rails application in the current directory.

Copy and paste the following line into your projects Gemfile on `line 30`. 

```ruby
group :production do
  gem 'pg', '~> 0.21' # for Heroku deployment
  gem 'rails_12factor'
end
```

and move 
```ruby 
gem 'sqlite3' 
```
from line 9 to the 
```ruby 
group :development :test 
```
in the Gemfile. 

Whenever you start working on a Rails project, the first thing you should do is to run Bundler, to make sure all the app's gems are installed.  Switch to the app's root directory and run 
```ruby
bundle config set --local without 'production'
bundle install

```
You only need to specify `without production` the first time, as this setting will be remembered on future runs of Bundler for this project.

At this point you should be able to run the app locally
```ruby
rails server -b 0.0.0.0
```
and navigate to `http://localhost:3000` in your browser.  

Note: If you stop the server by hitting control-C, you will no longer be able to visit the Ruby on Rails site. Start the server again by repeating the last command. 

Before you commit you may need to set up SSH key https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

Lastly, push the new application to Github. (You will need to run the git commands every time you want to push code to GitHub.) 
```sh
$ cd /root/{YOURPOJECTNAME}
$ git add -A
$ git status #Make sure all the new files are tracked AND on stage for being committed!!
$ git commit -m "Init"
$ git push
```
