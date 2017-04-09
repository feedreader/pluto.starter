# Sample Planet Starter Template Pack


See the [Pluto Planet Guide (Book Edition)](https://feedreader.github.io), that is,
the official documentation
for how to design your own template packs.



## Questions 'n' Answers

**Q: Why use [`planet.starter.html`](planet.starter.html.erb) for the filename (and NOT just simple `planet.html`)?**

A: By adding `starter` you can try other template packs (such as digest, hacker, top, etc.)
and the generated planet pages will NOT overwrite each other but will
live side-by-side in the same folder
(e.g. `planet.digest.html`, `planet.hacker.html` and so on) letting you try or serve
many styles / designs / themes.


**Q: What's [`starter.txt`](starter.txt) good for?**

A: The starter text file is the template pack(age) manifest (similar to `package.json` in the node.js world or `gemspec` in ruby)
listing all files (in plain text) that will get included.
The name of the file e.g. `starter` (without the `.txt` extension)
will get used as the name for the template option e.g. use `-t starter` or `--template starter`.






## Questions? Comments?

Send them along to the [wwwmake Forum/Mailing List](http://groups.google.com/group/wwwmake).
Thanks!
