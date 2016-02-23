Twitter Ebooks Bot Tutorial
=======================

![XKCD Twitter Bot](http://imgs.xkcd.com/comics/twitter_bot.png)

First things first hop on a machine running *NIX (OS X, Linux, etc)

- If you’re running OS X, open Terminal (found in ~/Applications/Utilities)
- If you're running Linux
    - If you're running Ubuntu, hit Ctrl-Alt+T
    - If you're not on Ubuntu I'd suggest figuring out how to open your Terminal before following this tutorial

Make sure you have Git installed.

On OS X, type `git` and hit enter. You should be prompted to install the command-line tools now. If you’ve already installed them your terminal will give you a brief explanation of git and its usage.

On Linux you should already have git installed.

[mispy](https://github.com/mispy) has my favourite ebooks code so I suggest cloning [their example](https://github.com/mispy/ebooks_example). It works fantastically.

```
git clone git@github.com:mispy/ebooks_example nulljosh_ebooks
cd nulljosh_ebooks/
```

Then you’ll want to install all of the dependencies (which are in Ruby)

```
sudo bundle install
```

Note: This `sudo` trick is a hack and I would suggest against it for them most part. The only reason I’m adding it here is I assume most of you will not touch Ruby again on your machines. If you’re planning on using Ruby in the future, or if you have before, set up a Ruby environment and fix gem permissions, then run this command without root privileges as a less hack-ey method.

Once the dependencies (gems) are installed, [npm](http://nodejs.org/download/) will be the next thing you’ll need installed.

With npm installed you can install a module [Kirby](https://twitter.com/hbkirb) made. You may have to kill Terminal first before running this (remember to `cd` back into your project.)

```
sudo npm install -g twauth
```

Note: Again, the `sudo` command is a hack. Same reasons apply here.

We’ll use twauth to essentially bypass Twitter’s phone verification, which they have in place to prevent users from abusing apps.

Now would be a good time to [create a Twitter account for your bot](https://twitter.com/signup). Make sure the email is confirmed. Then [sign up for a Heroku account](heroku.com), which you’ll be using to deploy your bot to-- unless you have your own server in which you can do that yourself. Once you have a Heroku account, [download (and install) the Heroku Toolbelt](https://toolbelt.heroku.com/). Once that's done, login to Heroku through Terminal:

```
heroku login
```

Now pertaining to what I mentioned earlier about bypassing Twitter’s phone authorization, we’re going to use Tweetbot’s leaked keys to be doing so :sweat_smile:

```
twauth --key=v8xVBZlXBp2AJoWI3VjDjzDkC --secret=Wpoom4N6tpTgfywzCt6y83gvZubbYoT0vL0V8FXzhyXA74218D
```

Your terminal will now provide you with a link to follow. Open it, sign in, and you should get an error message. This is expected. Scan the URL--you should get something like this:


```
https://push.tapbots.com/tweetbot/3/callback?oauth_token=sdgf876f98d7hlhfds9&oauth_verifier=4Wg5gzPhxcWrtfgee6Dgg8GwPgahhCRD
```

Copy the value of `&oauth_verifier` is-- in this case `4Wg5gzPhxcWrtfgee6Dgg8GwPgahhCRD`. Go back to your terminal and paste this in as your “pin number”. Hit enter and your terminal should respond with two OAuth keys-- one public, one private. Keep this terminal window open or copy the keys down-- We’ll be using them in a minute


- Open `bots.rb`
  - On line 22 assign  `self.consumer_key` to `v8xVBZlXBp2AJoWI3VjDjzDkC`
  - On line 23 assign `self.consumer_secret` to `Wpoom4N6tpTgfywzCt6y83gvZubbYoT0vL0V8FXzhyXA74218D`
  - Delete line 24 unless you have a reason to keep it.
  - On line 131 and change "abby_ebooks" to what your twitter bot username is (username_ebooks, etc)
  - One line 132 assign `bot.access_token` to
the first oauth key you got from twauth (the public one)
  - On line 133 assign `bot.access_token_secret` to the second key you got (your oauth private).
  - On line 135 assign `bot.original` to the username you want to base your ebooks off of (probably your main twitter username)

Flip back to Terminal and make sure you're still in your ebooks folder. Now you can generate an archive from your tweets.

```
export username=your_original_twitter_username
ebooks archive $username corpus/$username.json
ebooks consume corpus/$username.json
```

Now comes the unveil-- we want to test that the bot is working alright. We can use Heroku’s `forman` command for that:

```
foreman start
```

Try tweeting your bot now, or maybe follow it. Everything should be working.

We’re almost finished now-- we just want to push our bot to Heroku’s servers. First, initialize the git repository, then add all of your work, and commit it:

```
git init
git add -A
git commit -m "Initial Commit"
```

Heroku works with git quite nicely so you just need to create it, give it Heroku's remote, and push it. Also, make sure your Heroku server has an instance of the app.

```
heroku create
heroku ps:scale worker=1
git push heroku master
```

If you have any questions feel free to [tweet me](https://twitter.com/nulljosh).

© 2016 Joshua Trommel
