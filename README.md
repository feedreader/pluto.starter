
# Planet Pluto Quick Starter Kit

Welcome to Planet Pluto.
(Auto-)build your own (static) planet news site from web feeds.



## Step 0: Download and Unpack (or Clone)

To get started:

Option I) Download (that is, click on the green "Clone or download" button on the right side and than "Download ZIP") 
and unpack the zip archive.

Or

Option II) Use git and clone this repo e.g.

    $ git clone https://github.com/feedreader/pluto.starter


## Step 1: Install the Planet Pluto Machinery / Tool

To install the planet pluto tools and libraries use ruby's built-in standard package manager / installer e.g.

    $ gem install pluto


## Step 2: Build the Starter Planet

Try:

    $ pluto help

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

    $ pluto build planet.ini -t starter -o build


This will

1) fetch all feeds listed in [`planet.ini`](planet.ini) and

2) store all entries in a local single-file SQLite database,
that is, `planet.db` in your working folder and

3) generate a planet web page, that is, `planet.starter.html` in your build folder
using the [`starter` template pack](planet-starter) in the `planet-starter` folder
using all feed entries from the local database.


Example (first time) console output:

```
pluto/1.2.3 on Ruby 2.1.5

db settings:
{:adapter=>"sqlite3", :database=>"./planet.db"}

-- create_table(:logs)
-- create_table(:props)
-- create_table(:activities)
-- create_table(:sites)
-- create_table(:subscriptions)
-- create_table(:feeds)
-- create_table(:items)

dump >planet.ini<:
{"title"=>"Planet Open Data News",
 "osm"=>
  {"title"=>"Open Street Map (OSM) News",
   "link"=>"https://blog.openstreetmap.org",
   "feed"=>"https://blog.openstreetmap.org/feed/"},
 "okfnlabs"=>
  {"title"=>"Open Knowledge Foundation (OKFN) Labs News",
   "link"=>"http://okfnlabs.org/blog",
   "feed"=>"http://okfnlabs.org/blog/feed.xml"},
 "schemaorg"=>
  {"title"=>"schema.org News",
   "link"=>"http://blog.schema.org",
   "feed"=>"http://blog.schema.org/feeds/posts/default"},
 "wikidata"=>
  {"title"=>"Wikidata News",
   "link"=>"http://blog.wikimedia.org/c/technology/wikidata",
   "feed"=>"http://blog.wikimedia.org/c/technology/wikidata/feed/"}}

Updating feed subscription >osm< - >https://blog.openstreetmap.org/feed/<...
Updating feed subscription >okfnlabs< - >http://okfnlabs.org/blog/feed.xml<...
Updating feed subscription >schemaorg< - >http://blog.schema.org/feeds/posts/default<...
Updating feed subscription >wikidata< - >http://blog.wikimedia.org/c/technology/wikidata/feed/<...

OK - fetching feed 'osm' - HTTP status 200 OK
** NEW | OpenStreetMap Featured Images
** NEW | OSM first to honour plate tectonics
** NEW | SotM 2018 Call for Venues
** NEW | Use of CC BY 4.0 licensed data in OpenStreetMap
...

OK - fetching feed 'okfnlabs' - HTTP status 200 OK
** NEW | Data Package Pipelines
** NEW | Case Studies for Frictionless Data
** NEW | Embulk at csv,conf,v2
** NEW | Using Data Packages with Pandas
...

OK - fetching feed 'schemaorg' - HTTP status 200 OK
** NEW | Schema.org 3.2 release: courses, fact-checking, digital publishing accessibility, menus and more...
** NEW | schema.org update: hotels, datasets, "health-lifesci" and "pending" extensions...
** NEW | GS1 Web vocabulary: welcoming the first schema.org external extension
** NEW | Schema.org: what's new?
...

OK - fetching feed 'wikidata' - HTTP status 200 OK
** NEW | Your October milestones include Wikidata’s 15 millionth item
** NEW | Wikidata, coming soon to a menu near you
** NEW | Developers gather in France for the 2015 Wikimedia Hackathon
** NEW | It’s time for some #tastydata
...

Merging template pack 'starter'
  Loading template manifest planet-starter/starter.txt...
  Merging to planet.starter.html...
  Loading template (from file) >planet-starter/planet.starter.html.erb<...
  Copying to css/planet.starter.css from planet-starter/css/planet.starter.css...
  Copying to i/feed-icon-10x10.png from planet-starter/i/feed-icon-10x10.png...
Done (in 0.42304 s).
Done.
```


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

**Q: How can I update the web feeds and (re)build the planet page(s)?**

A: Rerun the command:

    $ pluto build planet.ini -t starter -o build

That's it ;-) The pluto feed fetcher will use conditional HTTP get requests and content hash checks for web feeds etc.



**Q: For testing how can I (re)build the planet pages(s) WITHOUT fetching the web feeds?**

A: Use the merge command:

    $ pluto merge -t starter -o build

Note: You do NOT need to pass along the `planet.ini` configuration on merge - everything
(e.g. planet title, web feed subscriptions, etc.) is stored in the
local single-file SQLite database, that is, `planet.db` in your working folder.


**Q: How can I update the web feeds WITHOUT (re)building the planet page(s)?**

A: Use the update command:

    $ pluto update

Note: You do NOT need to pass along the `planet.ini` configuration on merge - everything
(e.g. planet title, web feed subscriptions, etc.) is stored in the
local single-file SQLite database, that is, `planet.db` in your working folder.


**Q: How can I install Pluto with a Gemfile and ruby's bundler "virtual env" manager and locked down versions of all dependencies?**

A: To install the planet pluto tools and libraries with "locked down" versions in a virtual / isolated
environment use ruby's bundler. Ruby's bundler requires a `Gemfile` to
know what you want to install. Add a Gemfile in the `pluto.starter/` "top-level" directory. 
Example:

``` ruby
source "https://rubygems.org"

gem "pluto"
```

Now you can

    $ bundle install

and this will fetch and install all libraries and 
generate a `Gemfile.lock` that lists all libraries
with all dependencies (recursive all the way down) and all versions locked down.

Note: If you use bundler and want to use the virtual / isolated environment 
you MUST always start `pluto` commands with `bundle exec`. Example:

    $ pluto help

becomes
    
    $ bundle exec pluto help

and

    $ pluto build planet.ini -t starter -o build

becomes
    
    $ bundle exec pluto build planet.ini -t starter -o build

and so on.


**Q: What packages for Debian (above a slim base image) allow the bundle install to succeed?**

A:  A sufficient set of packages for Debian (above a slim base image) 
to allow the `bundle install` to succeed is:

    git ruby-bundler sqlite3 sudo gcc make libsqlite3-dev ruby-dev

And a minimal Dockerfile looks like:

```
FROM debian:buster-slim

RUN apt-get update \
    && apt-get install -y --no-install-recommends --no-install-suggests \
	git ruby-bundler sqlite3 sudo gcc make

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    /usr/bin/passwd -d developer && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers  && \
    chown -R developer:1000 /home/developer/

USER developer
ENV HOME /home/developer


WORKDIR /home/developer

RUN git clone https://github.com/feedreader/pluto.starter ; chown -R developer pluto.starter

CMD ["/bin/bash"]
```

Contributed by / Thanks to [Nathan Wallach](https://github.com/taniwallach)




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
