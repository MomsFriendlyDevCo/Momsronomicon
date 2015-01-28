Hosting with DigitalOcean
=========================

Server provisioning
-------------------
To setup a micro Digital Ocean instance follow these steps:

1. Create a new Digital Ocean VM instance called `webX` (where 'X' is the next available number)
	* Select Singapore as the location
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
