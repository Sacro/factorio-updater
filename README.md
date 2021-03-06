This is an aid for [Factorio](http://www.factorio.com/) headless server owners.
It fetches update packages from factorio.com for you, so that you can then apply
the update with minimal downtime.


## Usage ##

This is a Python 2 script using a single non-standard library,
[Requests](http://requests.readthedocs.org/en/latest/).

To install the required dependency, you should need do no more than run `pip
install requests` (or, in case of emergency, `easy_install requests`). If this
does not work, you are encouraged to read the linked documentation and try to
figure out what's gone wrong.

---

From there, it's really simple: open a shell on the machine running your
headless server, fetch the updater script, and run it (try it with `--help`
first!). Here's an example session:

```
[narc@odin ~/src/factorio-updater]% python update_factorio.py --help
usage: update_factorio.py [-h] [-d] [-v] [-l] [-u USER] [-t TOKEN]
                          [-p PACKAGE] [-f FOR_VERSION] [-O OUTPUT_PATH] [-x]

Fetches Factorio update packages (e.g., for headless servers)

optional arguments:
  -h, --help            show this help message and exit
  -d, --dry-run         Don't download files, just state which updates would
                        be downloaded.
  -v, --verbose         Print URLs and stuff as they happen.
  -l, --list-packages   Print a list of valid packages (e.g., 'core-
                        linux_headless64', etc.).
  -u USER, --user USER  Your Factorio updater username, from player-data.json.
  -t TOKEN, --token TOKEN
                        Your Factorio updater token, also from player-
                        data.json.
  -p PACKAGE, --package PACKAGE
                        Which Factorio package to look for updates for, e.g.,
                        core-linux_headless64 for a 64-bit Linux headless
                        Factorio. Use --list-packages to fetch an updated
                        list.
  -f FOR_VERSION, --for-version FOR_VERSION
                        Which Factorio version you currently have, e.g.,
                        0.12.25.
  -O OUTPUT_PATH, --output-path OUTPUT_PATH
                        Where to put downloaded files.
  -x, --experimental    Download experimental versions, too (otherwise only
                        stable updates are considered).
[narc@odin ~/src/factorio-updater]% python update_factorio.py -l
Available packages:
        core-linux_headless64
[narc@odin ~/src/factorio-updater]% python update_factorio.py -p core-linux_headless64 -f 0.12.25 -x
Wrote /tmp/core-linux_headless64-0.12.25-0.12.26-update.zip, apply with `factorio --apply-update /tmp/core-linux_headless64-0.12.25-0.12.26-update.zip`
[narc@odin ~/src/factorio-updater]% cd ~/srv/factorio/bin/x64
[narc@odin ~/srv/factorio/bin/x64]% ./factorio --apply-update /tmp/core-linux_headless64-0.12.25-0.12.26-update.zip
[...stuff happens...]
[narc@odin ~/srv/factorio/bin/x64]% rm /tmp/core-linux_headless64-0.12.26-0.12.26-update.zip
```



## License ##

The source of **Factorio Update Helper** is Copyright 2015 Octav "narc" Sandulescu. It
is licensed under the [MIT license][mit], available in this package in the file
[LICENSE.md](LICENSE.md).

[mit]: http://opensource.org/licenses/mit-license.html


## Statistics ##

1 API key was invalidated during the development of this script.
