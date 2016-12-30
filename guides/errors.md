Common Errors
=============

NODE: Using Port 80
-------------------
By default on Linux systems all ports below 1024 are privileged (i.e. only available for root users).

If you wish to run a Node service that listens on Port 80 you will need to tell the Operating system that Node is allowed to do this.

1. Install `libcap2-bin` via your package manager of choice (On Ubuntu this would be the command `sudo apt-get install -y libcap2-bin`)
2. Instruct the Kernel that Node is allowed to use lower port numbers with the command `sudo setcap cap_net_bind_service=+ep /usr/bin/nodejs`



GULP: The 'ENOSPC' error
------------------------
`ENOSPC` usually means that you are out of *something*. Not necessarily disk space.

The MFDC default Gulp setup installs a lot of file watchers when running Gulp, these check to see if any files were updated and if so restart the gulp process. This allows you to code and the Gulp process to take care of recompiling scripts, CSS and other resources without you manually having to do so.

In order to do this Gulp uses the `fs.watch()` functionality (via the [chokidar](https://github.com/paulmillr/chokidar) module wrapper) which installs a watcher on every file and directory that is likely to change during the lifecycle of the project. Some operating systems have limited numbers of files that can be watched at any one time.

The `ENOSPC` error typically occurs when the operating system runs out of available file watcher handles.

**LINUX FIX**

To fix this issue on Linux run `echo 9999999 | sudo tee /proc/sys/fs/inotify/max_user_watches >/dev/null`.

This command should fix up Gulp *in the short term*.

To apply a more permanent fix:

1. Edit the `/etc/rc.local` (as root - e.g. `sudo pico /etc/rc.local`)
2. Go to the line ABOVE the `exit 0` which should be the last line of the file
3. Add the line `echo 9999999 >/proc/sys/fs/inotify/max_user_watches` (this should be above `exit 0`)


**[Back to Table of Contents](../README.md)**
