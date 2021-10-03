
## Part 2: Preparation: deploy to Heroku

First, make sure you are in the `cs3300` directory.

If you have deployed to Heroku before, just create a new app container with `heroku create`.  If this is your first time deploying to Heroku, you will need to do two things.  First, sign up for a free [Heroku account](http://heroku.com).  Then set up ssh keys to securely communicate with Heroku for app deployments.  Next install Heroku. The four basic commands you need are the following, but see the [Heroku page](https://devcenter.heroku.com/articles/heroku-cli) for more details.

```sh
$ ssh-keygen -t rsa
$ curl https://cli-assets.heroku.com/install.sh | sh
$ heroku login -i
$ heroku keys:add
```

Once your keys are set up (a one-time process), you should be able to create an "app container" on Heroku into which you'll deploy RottenPotatoes:

```sh
$ cd /root/{YOURPOJECTNAME}
$ git init 
$ heroku create --stack heroku-18 # If you miss this step you can run this command to set it `heroku stack:set heroku-18`
```

Heroku will assign your app a whimsical name such as `luminous-coconut-237`; once your app is deployed, you would access it at `http://luminous-coconut-237.herokuapp.com`.  You can login to the Heroku website if you want to change the name of your app.

Confirm the new git associations: `git remote -v`
You should ONLY see fetch and push associated with heroku. These links automatically are built when you ran `heroku create`.

```sh
$ git add -A
$ git commit -m "Pushing to heroku"
```

Finally, we deploy our app to Heroku:

```sh
$ git push heroku master
```

(You may see the  following warning the first time - it's fine---answer
"yes", and in the future you shouldn't see it anymore:)

    The authenticity of host 'heroku.com (50.19.85.132)' can't be established.
    RSA key fingerprint is 8b:48:5e:67:0e:c9:16:47:32:f2:87:0c:1f:c8:60:ad.
    Are you sure you want to continue connecting (yes/no)? 
    Please type 'yes' or 'no':

You will see some warnings, but none are critical in most cases.

Is the app running on Heroku?  If you navigate to the heroku URL that is printed at the end of the results from `git push heroku master` you'll get a "We're sorry, but something went wrong." error in the browser.  

We can get a hint as to why by running the following command:

```sh
$ heroku logs
```

which will show an error like:

```
ActionView::Template::Error (PG::UndefinedTable: ERROR:  relation "projects" does not exist
```

Just as we ran `rake db:migrate` and `rake db:seed` to do first-time database creation locally, we must also cause a database to be created on the Heroku side:

```sh
$ heroku rake db:migrate
```

Now you should be able to navigate to your app's URL.  `heroku open` opens your browser to that URL in case you forgot it, however this command does not work on code-esaas, where you will need to navigate to the relevant URL.

You will need to push your code everytime you make a change and re-run the database migration (if required). 
```sh
$ git add -A
$ git commit -m "Commit message"
$ git push heroku master
$ heroku rake db:migrate # If required
```


