Sample init scripts and service configuration for onyxd
==========================================================

Sample scripts and configuration files for systemd, Upstart and OpenRC
can be found in the contrib/init folder.

    contrib/init/onyxd.service:    systemd service unit configuration
    contrib/init/onyxd.openrc:     OpenRC compatible SysV style init script
    contrib/init/onyxd.openrcconf: OpenRC conf.d file
    contrib/init/onyxd.conf:       Upstart service configuration file
    contrib/init/onyxd.init:       CentOS compatible SysV style init script

Service User
---------------------------------

All three Linux startup configurations assume the existence of a "onyx" user
and group.  They must be created before attempting to use these scripts.
The macOS configuration assumes onyxd will be set up for the current user.

Configuration
---------------------------------

At a bare minimum, onyxd requires that the rpcpassword setting be set
when running as a daemon.  If the configuration file does not exist or this
setting is not set, onyxd will shut down promptly after startup.

This password does not have to be remembered or typed as it is mostly used
as a fixed token that onyxd and client programs read from the configuration
file, however it is recommended that a strong and secure password be used
as this password is security critical to securing the wallet should the
wallet be enabled.

If onyxd is run with the "-server" flag (set by default), and no rpcpassword is set,
it will use a special cookie file for authentication. The cookie is generated with random
content when the daemon starts, and deleted when it exits. Read access to this file
controls who can access it through RPC.

By default the cookie is stored in the data directory, but it's location can be overridden
with the option '-rpccookiefile'.

This allows for running onyxd without having to do any manual configuration.

`conf`, `pid`, and `wallet` accept relative paths which are interpreted as
relative to the data directory. `wallet` *only* supports relative paths.

For an example configuration file that describes the configuration settings,
see `share/examples/onyx.conf`.

Paths
---------------------------------

### Linux

All three configurations assume several paths that might need to be adjusted.

Binary:              `/usr/bin/onyxd`  
Configuration file:  `/etc/onyx/onyx.conf`  
Data directory:      `/var/lib/onyxd`  
PID file:            `/var/run/onyx/onyxd.pid` (OpenRC and Upstart) or `/var/lib/onyxd/onyxd.pid` (systemd)  
Lock file:           `/var/lock/subsys/onyxd` (CentOS)  

The configuration file, PID directory (if applicable) and data directory
should all be owned by the onyx user and group.  It is advised for security
reasons to make the configuration file and data directory only readable by the
onyx user and group.  Access to onyx-cli and other onyxd rpc clients
can then be controlled by group membership.

### macOS

Binary:              `/usr/local/bin/onyxd`  
Configuration file:  `~/Library/Application Support/onyx/onyx.conf`  
Data directory:      `~/Library/Application Support/onyx`  
Lock file:           `~/Library/Application Support/onyx/.lock`  

Installing Service Configuration
-----------------------------------

### systemd

Installing this .service file consists of just copying it to
/usr/lib/systemd/system directory, followed by the command
`systemctl daemon-reload` in order to update running systemd configuration.

To test, run `systemctl start onyxd` and to enable for system startup run
`systemctl enable onyxd`

NOTE: When installing for systemd in Debian/Ubuntu the .service file needs to be copied to the /lib/systemd/system directory instead.

### OpenRC

Rename onyxd.openrc to onyxd and drop it in /etc/init.d.  Double
check ownership and permissions and make it executable.  Test it with
`/etc/init.d/onyxd start` and configure it to run on startup with
`rc-update add onyxd`

### Upstart (for Debian/Ubuntu based distributions)

Upstart is the default init system for Debian/Ubuntu versions older than 15.04. If you are using version 15.04 or newer and haven't manually configured upstart you should follow the systemd instructions instead.

Drop onyxd.conf in /etc/init.  Test by running `service onyxd start`
it will automatically start on reboot.

NOTE: This script is incompatible with CentOS 5 and Amazon Linux 2014 as they
use old versions of Upstart and do not supply the start-stop-daemon utility.

### CentOS

Copy onyxd.init to /etc/init.d/onyxd. Test by running `service onyxd start`.

Using this script, you can adjust the path and flags to the onyxd program by
setting the BITCOIND and FLAGS environment variables in the file
/etc/sysconfig/onyxd. You can also use the DAEMONOPTS environment variable here.

### macOS

Copy org.onyx.onyxd.plist into ~/Library/LaunchAgents. Load the launch agent by
running `launchctl load ~/Library/LaunchAgents/org.onyx.onyxd.plist`.

This Launch Agent will cause onyxd to start whenever the user logs in.

NOTE: This approach is intended for those wanting to run onyxd as the current user.
You will need to modify org.onyx.onyxd.plist if you intend to use it as a
Launch Daemon with a dedicated onyx user.

Auto-respawn
-----------------------------------

Auto respawning is currently only configured for Upstart and systemd.
Reasonable defaults have been chosen but YMMV.
