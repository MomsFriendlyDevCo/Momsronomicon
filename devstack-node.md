NodeJS Dev Stack
================
The NodeJS Dev stack uses the following:

* Linux based web-hosting using dedicated VM instances
* HTML, CSS and JavaScript - the basics of web-page creation
* Git / [GitHub](https://github.com) - Code management
* [AngularJS](http://angularjs.org) - Frontend JS framework
* [NodeJS platform](http://nodejs.org) - Backend JS language
* [ExpressJS](http://expressjs.com) - Backend JS framework
* [MongoDB](https://www.mongodb.org) - Backend database
* [Monoxide](https://github.com/hash-bang/Monoxide) - Backend database wrapper. Functionally identical to [Mongoose](http://mongoosejs.com) (the same APIs can be used with no overhead). Monoxide fixes some common issues MFDC has encounted with Mongoose


Misc software components:

* [async-chainable](https://github.com/hash-bang/async-chainable) - Alternative to the [async](https://github.com/caolan/async) library that provides chainable support for complex workflows
* [gulp](http://gulpjs.com) - Build scripts, development environment and file monitoring
* [lodash](http://lodash.com) - General tooling library
* [mfdc-email](https://github.com/MomsFriendlyDevCo/mfdc-email) - Email sending library configured specifically for MFDC style projects
* [mfdc-repl](https://github.com/MomsFriendlyDevCo/mfdc-repl) - MFDC's own REPL command line interface. Especially useful for database access as it provides Babel support and user-friendly database access via Monoxide
* [moment](http://momentjs.com) - Date + time handling library
* [mongoose-scenario](https://github.com/hash-bang/Node-Mongoose-Scenario) - Initial database population and setup
* [monoxide](https://github.com/hash-bang/Monoxide) - In addition to its database access functionality, Monoxide can also provide [ReST server](https://github.com/hash-bang/Monoxide#rest-server) capabilities. This is especially useful with the front-end [Angular ngResource](https://docs.angularjs.org/api/ngResource) library
* [passport](http://passportjs.org) - User sessions and authentication

More about NodeJS projects can be found in the [Backend NodeJS projects](style-node.md) section.


Setting up a NodeJS environment
===============================
The following is a rough guide to getting NodeJS running on either a Linux or Windows machine. It is by no-means the only method to do so but we have found the following to function in the majority of cases.

If you have any feedback about this process or come across issues not outlined here please [get in touch](mailto:matt@mfdc.biz) so we can adjust this guide.


In general you will need the following components at a minimum to get a NodeJS project working:

1. NodeJS - The actual programming core
2. MongoDB - The NoSQL database, used for storage
3. NPM - Node Package Manager used by NodeJS to install NodeJS modules - you get this free with NodeJS
4. Git - The revision control system used to manage code
5. Gulp - The compiler + general dogsbody used to make everything run, installable via NPM


Linux Machines
--------------
More detailed instructions for setting up a full server environment can be found in the [MFDC Init Project](https://github.com/MomsFriendlyDevCo/Init). The [NodeJS setup scripts](https://github.com/MomsFriendlyDevCo/Init/blob/master/020-node) may be of particular use.

Setting up Node on Linux is a relatively straight forward affair since Linux is scriptable by its nature. The following guide assumes you are using a Debian / Ubuntu branded Linux setup. If you are not using a Debian based system you may wish to consult the guide for [your own distribution](https://nodejs.org/en/download/package-manager).


**Install NodeJS PPA via Node Source**

	curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -


**Actually install NodeJS + MongoDB + Git on your system**

	sudo apt-get install nodejs mongodb

Now you have NodeJS setup proceed to [Post NodeJS installation](#post-nodejs-installation).


Mac Machines
----------------
NodeJS can be installed [directly](https://nodejs.org/en/download/) but for other packages and features such as auto-updating it is recommended you use Brew:

1. Download and install [brew](http://brew.sh)
2. Open a Terminal (Spotlight > Utilities > Terminal)
3. Install NodeJS using Brew

	brew install node

4. Install MongoDB using Brew

	brew install mongodb

Now you have NodeJS setup proceed to [Post NodeJS installation](#post-nodejs-installation).


Windows Machines
----------------
NodeJS installation on Windows is a little tricker since you usually have to grab the individual components and install them from separate websites:

1. Download and install the [Windows NodeJS installer](https://nodejs.org/en/download)
2. Install [MongoDB](https://www.mongodb.org/downloads)
3. Install [Git](https://git-scm.com/downloads)
4. Add Git to the PATH variable (Start > Right click on Computer > Properties > Advanced System Settings > Environment Variables Button > Click Path > Edit > Add `;C:\Program Files\Git\bin` to the existing)
5. Update your `C:\User\Administrator\.gitconfig` file with the windows fix [here](http://stackoverflow.com/a/32080571/1295040)
6. Open a command prompt as Administrator (Start Menu > `cmd`) and install MongoDB as a Windows service using the following commands:

```
cd "Program Files\MongoDB\Server\3.0\bin"
mkdir c:\mongodb
mongod --dbpath=c:\mongodb --logpath=c:\mongodb\log.txt --install
net start mongodb
```

Now you have NodeJS setup proceed to [Post NodeJS installation](#post-nodejs-installation).


Post NodeJS installation
------------------------
This section assumes you now have a working NodeJS installation. Check this with `node --version` or `npm --versions`.


**Upgrade NPM to the latest version**

The NPM version that comes with the default NodeJS installation is usually out of date. Use NPM to update... well... NPM.

	sudo npm install -g npm


**Tweak some of the more annoying NPM settings**

The following will adjust NPM so its a little more informative when performing operations.

	# Be more vocal about what NPM is currently doing
	npm config set loglevel http

	# Use system-wide temporary directory (which should get cleared on restart)
	npm config set tmp /tmp/npm

	# Have NPM automatically save all `npm install` / `npm rm` states in the local package.json file
	npm config set save true

	# Turn off the bloody spinner animation
	npm config set spin false



**Install some commonly used global NPM packages**

The following global NPM packages are recommend but you will find your own preferred combination of tools over time.

	sudo npm install -g gulp pm2


**Project cloning and installation**

You should now have a working NodeJS + Mongo + Git + Gulp setup installed on your machine.

Cloning a project and getting started with development can differ from project to project - you should in most cases consult its own README.md file for specific instructions. Generally though the next steps take the following form:

	# Clone the repo
	git clone <project GIT URL>

	# Install all NPM components
	npm install

	# Setup a blank database
	gulp db

	# Boot the server
	gulp

In most cases Gulp should now take over running the day-to-day tasks. For the majority of projects Gulp should automatically recompile scripts, CSS or other resources as you edit them - allowing you to edit the files on the fly.


**[Back to Table of Contents](README.md)**
