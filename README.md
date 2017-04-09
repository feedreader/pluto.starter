
# Planet Pluto Quick Starter Kit

Welcome to Planet Pluto.
(Auto-)build your own planet news site from web feeds.



## Step 0: Download and Unpack (or Clone)

To get started:

Option I) Download (that is, click on the green "Clone or download" button on the right side and than "Download ZIP") and unpack the zip archive.

Or

Option II) Use git and clone this repo e.g.

    $ git clone https://github.com/feedreader/pluto.starter.git



## Step 1: Install the Planet Pluto Machinery / Tool

To install the planet pluto tools and libraries use
ruby's bundler e.g.

    $ cd pluto.starter
    $ bundle install

Ruby's bundler will use the [`Gemfile`](Gemfile) to
know what you want to install and will
generate a `Gemfile.lock` that will list all libraries
with all dependencies and versions locked down.


## Step 2: Build the Starter Planet

Try:

    $ bundle exec pluto help

to check up on your pluto installation. Resulting in:

```
NAME
    pluto - another planet generator (lets you build web pages from published web feeds)

SYNOPSIS
    pluto [global options] command [command options] [arguments...]

VERSION
    1.2.3

GLOBAL OPTIONS
    -c, --config=PATH - Configuration Path (default: ~/.pluto)
    --help            - Show this message
    -q, --quiet       - Only show warnings, errors and fatal messages
    --verbose         - (Debug) Show debug messages
    --version         - Display the program version

COMMANDS
    about, a      - (Debug) Show more version info
    build, b      - Build planet
    fetch, f      - Fetch feeds
    help          - Shows a list of commands or help for one command
    install, i    - Install template pack
    list, ls, l   - List installed template packs
    merge, m      - Merge planet template pack
    update, up, u - Update planet feeds
```


Now build the sample starter planet. Try:

    $ bundle exec pluto build planet.ini -t starter -o build


This will

1) fetch all feeds listed in [`planet.ini`](planet.ini) and

2) store all entries in a local single-file SQLite database,
that is, `planet.db` in your working folder and

3) generate a planet web page, that is, `planet.starter.html` in your build folder
using the [`starter` template pack](planet-starter) in the `planet-starter` folder
using all feed entries from the local database.

Open up `build/planet.starter.html` in your web browser
to see your planet web page. Voila!



## What's Next?

Now change the planet configuration in [`planet.ini`](planet.ini) to fit your needs.
Change the title and add your web feeds.

Look & feel. Change the starter templates in [`planet-starter`](planet-starter)
to your liking
or use a pre-made template pack / theme.

Happy planet!




## Questions 'n' Answers

**Q: How can I update the web feeds and (re)built the planet page(s)?**

A: Rerun the command:

    $ bundle exec pluto build planet.ini -t starter -o build

That's it ;-) The pluto feed fetcher will use conditional HTTP get requests and content hash checks for web feeds etc.



**Q: For testing how can I (re)built the planet pages(s) WITHOUT fetching the web feeds?**

A: Use the merge command:

    $ bundle exec pluto merge -t starter -o build

Note: You do NOT need to pass along the `planet.ini` configuration on merge - everything
(e.g. planet title, web feed subscriptions, etc.) is stored in the
local single-file SQLite database, that is, `planet.db` in your working folder.


**Q: How can I update the web feeds WITHOUT (re)builting the planet page(s)?**

A: Use the update command:

    $ bundle exec pluto update

Note: You do NOT need to pass along the `planet.ini` configuration on merge - everything
(e.g. planet title, web feed subscriptions, etc.) is stored in the
local single-file SQLite database, that is, `planet.db` in your working folder.



## References

- [Pluto Planet Guide (Book Edition)](https://feedreader.github.io) - Official Documentation
- [Pluto Planet Template Packs/Themes](http://planet-templates.github.io) - Blank, Digest, Hacker, Paper, Forty, News, Top 'n' More
- [Talk Notes - New Horizons - Build Your Own (Static) Planet News Site w/ Pluto (and Ruby)](https://github.com/geraldb/talks/blob/master/planet.md)


## License

![](https://publicdomainworks.github.io/buttons/zero88x31.png)

The `pluto.starter` scripts and templates are dedicated to the public domain.
Use it as you please with no restrictions whatsoever.


## Questions? Comments?

Send them along to the [wwwmake Forum/Mailing List](http://groups.google.com/group/wwwmake).
Thanks!
