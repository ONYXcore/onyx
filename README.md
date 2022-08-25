

ONYX Core [CRYPTOCURRENCY]
=====================================

What is ONYX?
----------------

ONYX is a decentralized peer-to-peer (P2P) digital currency and payment network powered by the open source blockchain protocol [YesPower]. With ONYX, users can pay anyone in the world at the fastest speed in 5 seconds, at the lowest cost compared to other digital assets.

To Build & Run
---------------------

```bash
./autogen.sh
./configure 
make
make install # optional
```

This will build ONYX-qt as well, if the dependencies are met.

Building
---------------------
The following are developer notes on how to build ONYX Core on your native platform. They are not complete guides, but include notes on the necessary libraries, compile flags, etc.

- [Dependencies](doc/dependencies.md)
- [macOS Build Notes](doc/build-osx.md)
- [Unix Build Notes](doc/build-unix.md)
- [Windows Build Notes](doc/build-windows.md)
- [OpenBSD Build Notes](doc/build-openbsd.md)
- [NetBSD Build Notes](doc/build-netbsd.md)
- [Gitian Building Guide](doc/gitian-building.md)

 `ONYX.conf` Configuration File
 ---------------------
The configuration file is used by `ONYXd`, `ONYX-qt` and `ONYX-cli`.

All command-line options (except for `-?`, `-help`, `-version` and `-conf`) may be specified in a configuration file, and all configuration file options (except for `includeconf`) may also be specified on the command line. Command-line options override values set in the configuration file and configuration file options override values set in the GUI.
The ONYX.conf file configurations:
```bash
server=1
daemon=1
listen=1
rpcuser=ONYX
rpcpassword=pass
[You can generate RPCauth in /share/rpcauth]
```

## Configuration File Path

The configuration file is not automatically created; you can create it using your favorite text editor. By default, the configuration file name is `ONYX.conf` and it is located in the ONYX data directory, but both the ONYX data directory and the configuration file path may be changed using the `-datadir` and `-conf` command-line options.

The `includeconf=<file>` option in the `ONYX.conf` file can be used to include additional configuration files.

### Default configuration file locations

Operating System | Data Directory | Example Path
-- | -- | --
Windows | `%APPDATA%\ONYX\` | `C:\Users\username\AppData\Roaming\ONYX\ONYX.conf`
Linux | `$HOME/.ONYX/` | `/home/username/.ONYX/ONYX.conf`
macOS | `$HOME/Library/Application Support/ONYX/` | `/Users/username/Library/Application Support/onyx/onyx.conf`

You can find an example ONYX.conf file in [share/examples/ONYX.conf](/share/examples/onyx.conf).

License
-------

ONYX Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/ONYXcore/ONYX/tags) are created
regularly to indicate new official, stable release versions of The ONYX Core.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.


Useful links
============

* Website:        http://onyx.run/
* BlockExplorer:  http://explorer.onyx.run/
* EU Pool:        http://pool-eu.onyx.run/
* US Pool:        http://pool-us.onyx.run/
* AS Pool:        http://pool-as.onyx.run/
* Discord:        https://onyx.run/discord/
* Telegram:       http://onyx.run/telegram/


