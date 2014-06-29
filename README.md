ebooks tutorial
===============

who wants to learn how to make a twitter ebooks
account?

requirements
------------
- a computer, preferably running OS X or Linux
(Windows' "command prompt" is an utter joke)
![screenshot](http://i.imgur.com/WTCa7fa.png)

- [ruby](https://www.ruby-lang.org/), which can easily
  be installed on OS X by downloading and opening
  [Xcode](https://developer.apple.com/xcode/). On Linux, you can
  install ruby with `sudo apt-get install ruby`.

    - i also heavily recommend installing [rvm](https://rvm.io)
    (I should basically make this a requirement,
      but there are ways around it).
      install rvm (and ruby) with
      `\curl -sSL https://get.rvm.io | bash -s stable`
      (if you're on Linux and you don't have curl, `sudo apt-get install curl`)
      first, run `rvm get stable --auto-dotfiles`, because rvm needs to be added
      to your `$PATH`.
      second, this project uses ruby v1.9.3, and you'll probably have the newest
      version of ruby, so run `rvm install ruby-1.9.3-p547` to install that.
      you should be all good until later, when you start working
      in your directory.

- it also might help to learn some basic command-line stuff,
but that's up to you to decide


steps
-----

1. ### open your Terminal
(on OS X, it's in `Applications/Utilities`. if you're running
Linux and you don't know where your Terminal is, you probably
shouldn't be running Linux.)
![screenshot](http://i.imgur.com/g0Fz4TZ.png)

2. ### it probably won't look like mine, but that's totally fine.
everything i do in this tutorial should work for you the same way.
![screenshot](http://i.imgur.com/Kmg9j0T.png)

3. ### `cd` into your Desktop
  ```bash
  $ cd Desktop/
  ```
  ![screenshot](http://i.imgur.com/Y2HDiGq.png)

4. ### install the [twitter_ebooks gem](https://github.com/mispy/twitter_ebooks)
  ```bash
  $ gem install twitter_ebooks
  ```
  ![screenshot](http://i.imgur.com/IiYNiUX.png)

  - if you get a "permission denied" error of some sort,
    prepend `sudo` onto the command and try again
    ```bash
    $ sudo gem install twitter_ebooks
    ```
    ![screenshot](http://i.imgur.com/ZpdKKW1.png)

5. ### once the twitter_ebooks gem has been installed, create your application / bot
  ```bash
  $ ebooks new yourAppName
  ```
  ![screenshot](http://i.imgur.com/g11QOYL.png)

6. ### `cd` into your application / bot, and use ruby v1.9.3
  ```bash
  $ cd yourAppName/
  $ rvm use ruby-1.9.3-p547
  ```
  ![screenshot](http://i.imgur.com/FCUIDQz.png)

7. ### open the project in your favourite text editor
  for example,
  ```bash
  $ atom
  ```
  (just because i'm not using vim right now, doesn't mean
  I should be harshly judged)
  ![screenshot](http://i.imgur.com/VOZym4m.png)

  - alright, cool
  ![screenshot](http://i.imgur.com/I9uM48K.png)

8. ### open up the `bots.rb` file. this is basically
  the only file you'll have to worry about for your
  bot to work the way you want it to
  ![screenshot](http://i.imgur.com/sIWPRsg.png)

9. ### now you'll need to create a twitter account for the bot
  i recommend using https://www.guerrillamail.com for a
  quick and easy, disposable email
  ![screenshot](http://i.imgur.com/g6BKx55.png)

  - sign up, etc
  ![screenshot](http://i.imgur.com/c7N84MF.png)

  - confirm your email, etc
  ![screenshot](http://i.imgur.com/rO0wxy7.png)

10. ### go ahead and log into your new twitter account
    - the account might be suspended when you log in
    (because the disposable email is fake, and that
      violates twitter's policies)
    ![screenshot](http://i.imgur.com/oNOmATu.png)

    - if it is, just click "suspended accounts"
    and agree to twitter's crap about
    "not doing anything stupid again"

11. ### go to https://dev.twitter.com
    ![screenshot](http://i.imgur.com/WZmqMML.png)

    - sign in, etc

12. ### create a new app
    ![screenshot](http://i.imgur.com/2s5ESNw.png)
    ![screenshot](http://i.imgur.com/vc7GIDt.png)

    - for the application details:
      - the name is what will be shown here
      (if you have tweetbot)
      ![screenshot](http://i.imgur.com/OVNjtVk.png)

    - the description is just a description of your
    application. nobody except users who can access the account
    will see it (only you, unless you share your password or something)

    - the website doesn't matter. you can put your own website
    in there if you have one and if you care

    - leave the callback URL blank. it's not important
    for creating bots (the callback URL would be important if you wanted
      users to be able to log into your application and use it with
      their twitter accounts- i.e. a twitter client
      (like tweetbot or tweetdeck, etc))

    - scroll down and accept the terms, conditions, and all that jazz.
    then hit "Create your Twitter Application"
    ![screenshot](http://i.imgur.com/smMyg29.png)
    ![screenshot](http://i.imgur.com/zALpCn1.png)

13. ### set permissions
    you probably want your bot to be able to tweet
    (basically the main point of having an ebooks bot),
    go click "permissions" so that you can edit twitter's default permissions
    ![screenshot](http://i.imgur.com/WrZe44I.png)
    ![screenshot](http://i.imgur.com/aCbP5O2.png)

    check "Read, Write and Access direct messages",
    and click "Update settings"
    ![screenshot](http://i.imgur.com/EahCyma.png)

    [#cool](https://twitter.com/search?q=%23cool&src=typd).

14. ### grab the API and OATH keys

    the API and OATH keys are strings containing
    a bunch of random characters and numbers, and every
    individual application has them (well, API keys anyways).
    no two API or OATH keys are the same. having these will allow
    us to connect the code behind our bot to the actual bot

    - click "API Keys"
    ![screenshot](http://i.imgur.com/cqXA2jS.png)

    for the purpose of this tutorial, i'm going to be displaying
    my API keys, because blurring them out is pointless (this is a tutorial,
      not a bot i care about). aside from me doing this, this one time,
      **don't share your private keys *unless you want people to be able
      to access your bots*.**

    - copy your API key and API secret keys..
    ![screenshot](http://i.imgur.com/wXkNfw5.png)
    ..and paste them into `bots.rb`
    (`bot.consumer_key` and `bot.consumer_secret`)
    ![screenshot](http://i.imgur.com/Dt81qF0.png)

    - go back to your application in your browser,
    and scroll down until you see "Token Actions".
    click "Create my access token"
    ![screenshot](http://i.imgur.com/voh2sBe.png)
    ![screenshot](http://i.imgur.com/NdLt6Ze.png)

    - copy the tokens into your project as well
    (`bot.oauth_token` and `bot.oauth_token_secret`)
    ![screenshot](http://i.imgur.com/bgOBM1h.png)
    ![screenshot](http://i.imgur.com/7Qv1gLG.png)

    your bot should (finally) now be ready to start working with :)

15. ### set up heroku (for hosting your bot)
    you'll use heroku for hosting your bot.
    if you want to use your own server (if you have one),
    that's fine. i'm not going to explain how to do that though,
    because heroku is a lot easier (and saves your server RAM, etc)

    - sign up for a heroku account on https://heroku.com
    ![screenshot](http://i.imgur.com/n7uDGqD.png)
      - you'll need to verify your email, etc

    - download and install the [heroku toolbelt](https://toolbelt.heroku.com/)
    ![screenshot](http://i.imgur.com/ovUtJdU.png)

    cool. later on, when we push our code to heroku's servers,
    we'll need to log into the account that we've made

16. ### now you get to code stuff for your bot

    this is all ruby, so you might want to learn some basics.
    here's a demo application of something you might want to make (probably not)
    ![screenshot](http://i.imgur.com/aEOGAzj.png)

17. ### now you'll need [bundler](http://bundler.io)

    bundler is a gem that allows you to manage all of the gems
    that you require for your application through a file called "`Gemfile`"

    - install bundler

      ```bash
      $ gem install bundler
      ```
        ![screenshot](http://i.imgur.com/VPlxa6p.png)

        -  again, if you get "permission denied" errors, just prepend "`sudo`"
          ```bash
          $ sudo gem install bundler
          ```
          ![screenshot](http://i.imgur.com/H6dKETk.png)

      it should install no problem :)
      ![screenshot](http://i.imgur.com/Ni15JGV.png)

    - now we want to install all of the gems that have been added to
      the `Gemfile` (we didn't add these, they were automatically created
      when we created our application / bot with the twitter_ebooks gem / CLI)
      ```bash
      $ bundle install
      ```
      ![screenshot](http://i.imgur.com/TCGyMep.png)

        - I forgot to take a screenshot for it (:anguished:), but
        if you start getting a ton of "permission denied" errors,
        you know what to do:
        ```bash
        $ sudo bundle install
        ```

        everything should work no problemo. you should have
        all of these gems installed, so that's cool.
        ![screenshot](http://i.imgur.com/CMz3pSp.png)

        **side note:** if you check, there should also be a new file called `Gemfile.lock`.
        I forgot the grab a screenshot, but hopefully it's there for you. it's
        important for later when we push our code to Heroku.

        **this is where you can test and debug your app:**
        running `foreman start` will start up your bot without having to go
        through the hassle of pushing it all to Heroku's servers.

        ![screenshot](http://i.imgur.com/EUKKtzy.png)

        - foreman is great for bug fixing, etc, because you don't want to have to push your
        code to Heroku's servers every time you do something and want to check
        if something does (or doesn't do) what you want it to do. once you've run
        `foreman start`, try doing something with your bot (like following it),
        and it should do whatever you've specified (i.e.: follow back).
        *your bot should work by now* (if it doesn't,
        go back and check previous steps). press control-c to kill foreman's
        process when you're finished testing.

18. ### initialize [git](http://git-scm.com) and commit our changes

    git is the best [SCM](http://en.wikipedia.org/wiki/Source_code_management)
    available, and if you argue with that, you're wrong.

    - run `git`
    if you have git installed (if you've ever installed xcode and / or the
    dev tools required to use it, you should have git), then you should see
    a message like this
    ![screenshot](http://i.imgur.com/wdmqSOO.png)

    if you don't have git installed, you should get a message explaining how to
    install it. I don't have a screenshot for this, but it's
    a pretty straightforward task to complete.

    cool, so you should have git installed now.

    - now you need to initialize your project, add everything in the project
    to git's queue, and, last but not least, commit your changes
    ```bash
    $ git init
    $ git add -A
    $ git commit -m "Initial Commit"
    ```
    ![screenshot](http://i.imgur.com/lqirWjc.png)

    git is now initialized in your project, and your code (and files)
    should now be committed. everything is ready to be pushed to
    Heroku's servers.

19. ### push your code to heroku

    - create your Heroku server
    ```bash
    $ heroku create
    ```
    ![screenshot](http://i.imgur.com/Kh5hkXm.png)

    - now push your code to Heroku's servers (I took this screenshot prematurely
      (heh), so there will be a lot more text / logs that come after the
      "runnning bundle install", etc, so don't worry about that)
      ```bash
      $ git push heroku master
      ```
    ![screenshot](http://i.imgur.com/8RAtQx9.png)

    once everything has been pushed, your bot should work :D

20. ### wrapping up

    there are always a couple of things that might not work
    in a project like this (and this scale), so here are a couple of things
    you can try if things aren't working for you.

    - edit the `Procfile`

      the `Procfile` is the file that is run
      as soon as you push your code to Heroku's server.
      it should have the code required to get your bot started.
      the twitter_ebooks CLI automatically generates this for you,
      but sometimes, removing the "start" in it fixes things up
      ![screenshot](http://i.imgur.com/NqK3Lve.png)
      ![screenshot](http://i.imgur.com/hgTLuAl.png)

      ..and of course, don't forget to push those changes to git,
      and then push the code to your Heroku server

      ![screenshot](http://i.imgur.com/7L80zVK.png)

    - reset the dynos for your Heroku server

      i don't know why this helps, but sometimes it does.
      (i forgot to grab screenshots for this. sorry. :bird:)

      ```bash
      $ heroku ps:scale worker=1
      $ git push heroku master
      ```
