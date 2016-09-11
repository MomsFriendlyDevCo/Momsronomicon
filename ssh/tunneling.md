Linux / Mac SSH Tunneling
=========================
This guide is intended as a reference to allow remote access to *your* Linux or Mac PC from MFDC.

The basic process of tunneling is:

1. Your computer dials into a common, shared server which is accessible by both parties
2. The connection formed is a normal SSH session but with reverse tunneling enabled - i.e. form a connection *back* from the shared server to your own laptop
3. The person wishing to connect to your PC connects to the shared server then dials though it into your PC


Setting up the credentials
--------------------------
To form a tunnel the shared server needs an account for you to connect to.

Please copy the contents of the file `~/.ssh/id_rsa.pub` into an email. The easiest way copy this to clipboard on a Linux machine is the command `xsel -ib <~/.ssh/id_rsa.pub`

**NOTE 1:** If this file does **not** exist you will need to create it with the command `ssh-keygen -f "$HOME/.ssh/id_rsa" -t rsa -N ''`

**NOTE 2:** In order to dial *in* to your machine you will need an OpenSSH server running. If you do not have one or are unsure, run `sudo apt-get install -y openssh-server`. If the server is already installed it will exit without doing anything.

MFDC will then need to create an account on the shared server which you can dial into.


Creating the tunnel
-------------------
An SSH tunnel is created by running the following command:

	ssh zapp.mfdc.biz -R 2222:localhost:22

The above command connects to the publicly available MFDC office server ("Zapp") then forms a reverse tunnel where port 2222 on Zapp is tunneled into your own PC port 22.

**NOTE:** Closing the connection (either by typing `exit` or pressing `Ctrl + D`) will close the tunnel.


Configuring a tunnel alias (optional)
-------------------------------------
If its likely you are going to be needing a tunnel often you can make an entry in your SSH config which should make setting up a tunnel easier.

Edit the file `~/.ssh/config` (create it if it doesn't exist) and add the entry:

	Host zapp
		Hostname zapp.mfdc.biz
		RemoteForward 2222 localhost:22

It is now possible to setup the connection by running `ssh zapp`. Change the `Host zapp` line if you wish to call the connection something else.


**[Back to Table of Contents](../index.md)**
