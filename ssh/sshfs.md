SSH-FS - Remote mounting with SSH
=================================

FIXME: Content to come


**[Back to Table of Contents](../README.md)**

### MacOS

#### Make sure you have an SSH key
1. Check if you already have an SSH key. You can do this by running `ls -al ~/.ssh` in Terminal. Look for one named: `id_rsa.pub`, `id_dsa.pub`, `id_ecdsa.pub`, `id_ed25519.pub`, etc.
    - You can generate one be running in Terminal: `ssh-keygen -t rsa -b 4096`
2. Copy your public SSH key. Run `cat ~/.ssh/id_rsa.pub` in Terminal and copy the output.
3. Pass this to the administrator to add to the remote machine to allow your device to connect remotely with.

#### Install MacFUSE and SSHFS
1. Go to: https://osxfuse.github.io/ and download the stable releases of MacFUSE and SSHFS.
2. Run both downloaded `.dmg` files and go through the wizard process to install them.
3. After installing, you will encounter one or more of the following scenarios:
    - Your system will prompt you that it needs a restart, go ahead restart your machine.
    - You may need to allow the extensions or you will be prompted to. Check this by going to: System Preferences > Security & Privacy and see if there is a message: Allow the system extension from developer "Benjamin Fleischer".
    - On a Mac with Apple silicon, you may first need to use Startup Security Utility to set the security policy to Reduced Security and select the “Allow user management of kernel extensions from identified developers” checkbox. (see https://support.apple.com/en-au/guide/mac-help/mchl768f7291/mac).

#### Mount remote drive
1. Create an empty directory to mount the remote drive in. `mkdir /Users/steve/Desktop/remote` will create a folder called "remote" on your Desktop. Of course, change **steve** in the path to be your Mac user name.
2. Run `sshfs user@127.0.0.1:/ /Users/steve/Desktop/remote -o volname=remote -o follow_symlinks`, replace **user** with your assigned username, **steve** with your Mac user name **127.0.0.1** with the remote machine's IP (or URL) and **remote** with what you'd like to name the mounted drive.

#### Persisting mounted drive
TODO
