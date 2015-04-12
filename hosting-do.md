Hosting with DigitalOcean
=========================

Generic server provisioning
---------------------------
To setup a Digital Ocean instance with Node support follow the below steps. If the VM is intended to host a LAMP stack see the next section for tips on zPanel instance setups.

1. Create a new Digital Ocean VM instance
	* Name the machine after the TLD prefix of the domain (e.g. if the domain is example.com the name shoudl be 'example')
	* Generally the smallest size VM is acceptable in most cases
	* Ensure that 'Enable Backups' is selected
	* Select Singapore as the location
	* Ubuntu is recommended as the OS
	* Add all SSH access keys to the new VM instance

2. SSH into the new machine and run the following to grab the usual set of init scripts

	sudo apt-get install -y git
	git clone git@github.com:MomsFriendlyDevCo/Init.git
	cd Init

3. Run the init rule appropriate to the server role. In the majority of cases this will be:

	./ROLE-server-node

4. Setup the A record DNS of the domain to point at the IP of the VM

5. Clone the git repo of the site you wish to host into the `root` home directory:

	git clone <repo>
	cd <repo-dir>

7. Run whatever setup scripts are required for the project, these should be listed in the repo `README.md` file but are *usually*:

	npm install
	bower install
	gulp db

6. Use [Forever](https://www.npmjs.com/package/forever) to run the main script

	forever start server.js

7. Check that the website now works correctly


zPanel web hosting
==================
[zPanel](http://www.zpanelcp.com) is a Free and Open Source equivelent to cPanel which allows generic hosting of LAMP based websites.


zPanel Server provisioning
--------------------------
To setup a micro Digital Ocean instance follow these steps:

1. Create a new Digital Ocean VM instance
	* Name the machine `webX` (where 'X' is the next available number)
	* Generally the smallest size VM is acceptable in most cases
	* Ensure that 'Enable Backups' is selected
	* Select Singapore as the location
	* Ubuntu is recommended as the OS
	* Add all SSH access keys to the new VM instance

2. Add the DNS entry for the newly created box in the Digital Ocean DNS config area. The format should be `webX.momsfriendlydev.co` with the IP of the newly created instance.

3. Wait until the DNS propagates (i.e. you can both ping the newly created domain from your local machine *and* from the VM)

4. SSH into the new box and run the following deploy script:

```bash

echo "Installing standard DEB packages..."
sudo apt-get update

sudo apt-get install --force-yes -y \
cron-apt \
moreutils \
nagios-plugins \
wget \


echo "Setting suitable PHP options..."
sudo perl -pi -e 's/^display_errors = .*$/display_errors = On/g' /etc/php5/apache2/php.ini
sudo perl -pi -e 's/^short_open_tag = .*$/short_open_tag = On/g' /etc/php5/apache2/php.ini
sudo perl -pi -e 's/^upload_max_filesize = .*$/upload_max_filesize = 32M/g' /etc/php5/apache2/php.ini


echo "Downloading zPanel install script..."
wget 'https://raw.githubusercontent.com/zpanel/installers/master/install/beta/Ubuntu-14_04-LTS/ubuntu-14.04-LTS-apache2.4.9-php5.5.14.sh'
```

5. Add the Nagios entry on Zapp to monitor the server remotely

6. Run `bash ubuntu*.sh` to setup zPanel - make sure you do this inside a `screen` session so its disconnect safe
	* The timezone is `Australia/Brisbane`
	* The domain name will be `webX.momsfriendlydev.co`
	* Sometimes the installer appears to stall after 'Restarting Apache' this is because the DNS system requires entropy to generate random keys. Hitting random keyboard keys will populate this

7. Note down and email Matt with the created account details when the process completes - the details are also saved in `~/passwords.txt`


Creating domains
----------------
To setup a hosting account follow these steps:

1. Login to the zPanel of the least populated web server - typically the domain will be something like `webX.momsfriendlydev.co` (where X is a number)

2. Click `Reseller > Manage Clients` and create a new account
	* Note down the username and password created and send to Matt
	* The Group will be `Users` in most cases

3. Should the user require FTP access click `File Management > FTP Accounts` and create an account with the same details as above


Setting up email
----------------
To setup a users email follow these steps:

1. Login to the zPanel of the **User Account**. This login will *never* be `zadmin` it will always be the user account created when the domain was setup.

2. Click `Mail > Mailboxes` and enter the email details
	* Note down the details used and send to Matt



**[Back to Table of Contents](README.md)**
