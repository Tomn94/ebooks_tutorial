an easier way to make ebooks than the last walkthrough
========================================

grab a computer running OS X or Linux or Unix in general really. this tutorial will mostly be for
Mac but any Unix system will work. if you're using Linux you should be able to figure this out by the
general steps.

- if you're on a Mac, open Terminal (found in ~/Applications/Utilities)
- if you're running Linux find your own damn Terminal

get comfortable
```
cd Desktop/
```

if you're sporting a Mac just type in

```
git
```

and hit enter and it should ask you to install the command line tools. sweet, do that
if it gives you info on git you already have command line tools probably. even better

if you have Linux you probably have git

[mispy](https://github.com/mispy) has my favourite ebooks code so if you wanna just clone [her example](https://github.com/mispy/ebooks_example) that'd make things a lot easier. it's full functional :) then `cd` into the directory

```
git clone https://github.com/mispy/ebooks_example > your-ebooks-name_ebooks
cd your-ebooks-name_ebooks
```

since there's a Gemfile just

```
sudo bundle install
```

this'll install all the gems you need to get this shit on the road :smile:

once you have the gems installed, install [npm](http://nodejs.org/download/)

with npm installed you can install a module Kirby made from a gist i think? you might have to kill Terminal first before running this (remember to `cd` back into yoru dirs :aerial_tramway:)

```
npm install -g twauth
```

it basically lets you bypass verifying your twitter account with a phone number before you can make an app and get your keys and stuff, which you need

while you're at it, [make a twitter account](https://twitter.com/signup) for your bot. confirm the email and make sure everything goes well :) then [grab a Heroku account](heroku.com), which you'll use to throw your bot on. unless you have your own server in which you can do that yourself. once you have a Heroku account, [download (and install) the Heroku Toolbelt](https://toolbelt.heroku.com/). once that's done, login to Heroku through Terminal

```
heroku login
```

Heroku will ask you for your credentials and once you throw em in you're good to go


now grab your keys. make sure these keys are correct. use tweetbot's leaked consumer keys!! :sweat_smile:

```
twauth --key=v8xVBZlXBp2AJoWI3VjDjzDkC --secret=Wpoom4N6tpTgfywzCt6y83gvZubbYoT0vL0V8FXzhyXA74218D
```

your terminal will (should) give you a link to visit. visit it, sign in, and you should get an error message. no worries, check the url, you should get something like this


```
https://push.tapbots.com/tweetbot/3/callback?oauth_token=asdflkjhdsaf&oauth_verifier=asdlfkhjsdafsdf
```

copy what the &oauth_verifier is, in this case "asdlfkhjsdafsdf".  go back to your terminal and paste this in. this is your "pin number"

hit enter and you should get oauth keys- one public, one private

keep this terminal window open or copy the keys or something. we'll use them in a minute


- open `bots.rb`
  - on line 22 assign  `self.consumer_key` to `v8xVBZlXBp2AJoWI3VjDjzDkC`
  - on line 23 assign `self.consumer_secret` to `Wpoom4N6tpTgfywzCt6y83gvZubbYoT0vL0V8FXzhyXA74218D`
  - delete line 24 unless you have a reason to keep it.
  - on line 131 and change "abby_ebooks" to what your twitter bot username is (username_ebooks, etc)
  - one line 132 assign `bot.access_token` to
the first oauth key you got from twauth (the public one)
  - on line 133 assign `bot.access_token_secret` to the second key you got (your oauth private). - on line 135 assign `bot.original` to the username you want to base your ebooks off of (probably your main twitter username)

radical :snowboarder:

jump back into your Terminal now and make sure you're still in your ebooks folder. now you can generate an archive from your tweets.

```
export username=your_twitter_username
ebooks archive username corpus/$username.json
ebooks consume corpus/$username.json
```

now to test your ebooks and make sure it's working good and golly

```
foreman start
```

try tweeting your bot now, say something passive agressive and then block it or something.

if it's working all good and replying to you and shit you can throw it on Heroku and get it the fuck off your machine

Heroku works with git so nicely so you just need to throw it on Heroku's remote

```
git init # init git, RHYMES
git add -A
git commit -m "Initial Commit"
git push heroku master
```

your bot should be working now :))

if it's not try this

```
heroku ps:scale worker=1
git push heroku master
```

if it's still not [tweet me](https://twitter.com/nulljosh) and ask me nicely to help you

© 2k15 josh
