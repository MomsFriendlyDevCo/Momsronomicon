SSH Keys
========
This guide is intended as a reference to generate SSH keys.

An SSH key is like a password but is mega secure. Its job is to allow your machine (desktop, laptop etc.) to automatically log into a remote machine without having to enter passwords and so on.

An SSH key is made up of two parts. The below paths assume you are on a Mac or Linux machine. While Windows does support SSH keys its a painful process that is outside the scope of this guide.

* `~/.ssh/id_rsa` - This is your *private* key. You should never share this with anyone.
* `~/.ssh/id_rsa.pub` - This is your *public* key. When people refer to "give me your SSH key" they are refering to the contents of this file. Copying or sharing the contents of this file is perfectly safe.


Generating an SSH Public Key
----------------------------
If you dont already have a `~/.ssh/id_rsa.pub` file you need to generate one.

The easiest way of doing this is to paste the following command:

	ssh-keygen -f "$HOME/.ssh/id_rsa" -t rsa -N ''

What this does is generates a new RSA key specifying no-password. If you want to walk though the process step-by-step you can use the command `ssh-keygen` and answer the prompts youself.


**[Back to Table of Contents](../index.md)**
