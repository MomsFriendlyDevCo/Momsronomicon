PHP / CodeIgniter projects
==========================
PHP and CodeIgniter is being phased out here at MFDC but there are still a lot of legacy software projects around which may require maintenance or new additions.


PHP
---
PHP is one of the two major programming languages at MFDC (the other being the front-end JavaScript code). While likely to change in the future (to NodeJS), PHP remains with us as our primary development language.

Ok lets get the bad things out of the way to start with. There are [lots of faults with PHP](https://maurus.net/resources/programming-languages/php) but lets just concentrate on those that effect us as a company and you as a dev:

* [Functions, parameters and return values are inconsistently named](http://tnx.nl/php.html#args), not in a logical style or just plain suck. Is it [Needle, Haystack](http://au1.php.net/manual/en/function.explode.php) or [Haystack, Needle](http://au1.php.net/manual/en/function.strpos.php), is it [Compound function names](http://au1.php.net/manual/en/function.isset.php) or [Underscore function names](http://au1.php.net/manual/en/function.is-array.php). The language is a mess.
* Object Orientation is just **bad** - While classical OO techniques such as inheritance do exist, more modern techniques such as introspection or [Duck Punching](https://en.wikipedia.org/wiki/Duck_punching) are either unsupported or involve workarounds which are painful to code.
* The PHP organisation committee appear to be taking whatever the opposite of LSD is - something that makes you increasingly more boring and pedantic. Their rejection of some perfectly sensible additions to the language is [nothing short](https://wiki.php.net/rfc/keywords_as_identifiers) of [baffling](https://wiki.php.net/rfc/named_params).


And now for the good news:

* PHP is extremely easy to learn if you have a rough background in *any other* language.
* It is entirely output agnostic allowing you to output HTML just as easily as JSON, XML, [images](http://au1.php.net/manual/en/book.image.php) or even [Flash](http://au1.php.net/manual/en/book.swf.php) (remember that!?).
* *Because* the Object Orientation is so bad (see above) most of the internal functionality is plain flat (admittedly globally namespaced) functions. Need to calculate an [MD5 hash](http://au1.php.net/manual/en/function.md5.php), the function is called `md5()` no external `import`, `require`, `uses` or other means of bringing in a module is required. No hunting though object stacks or trying to remember the exact name of the library like in [Python](https://docs.python.org/2/library/hashlib.html) or [Perl](https://metacpan.org/pod/Digest::MD5) is required. Don't believe me? The function to return the local date format using JavaScript/WinJS is `Windows.Globalization.DateTimeFormatting.DateTimeFormatter.shortDate.format()`, in PHP its `date()` and you pass it a [format](http://au1.php.net/manual/en/class.datetime.php#datetime.constants.types).
* Cross platform - PHP is hands down the most cross platform language this author (MC) has ever used. Yes this is a controversial thing to say, yes I can back it up. Bring it on.


In conclusion, what usually happens, as with any other language that has its horrible bits (I'm looking at *you* JavaScript) is someone comes along and builds a framework over the top to abstract away the horribleness of the general language. Enter CodeIgniter...


CodeIgniter
-----------
> PHP is a minor evil perpetrated and created by incompetent amateurs, whereas Perl is a great and insidious evil, perpetrated by skilled but perverted professionals
> - Jon Ribbens

CodeIgniter generally follows a pretty strict layout (all controllers live in `/application/controllers`, all models in `/application/models` etc.) so there isn't too much to add here except various tips we've picked up over the years:

* Controllers should always be named after plural nouns (e.g. 'users', 'devices', 'widgets', 'pages'). This usually approximates the database table structure as each controller should generally have a CRUD structure (see next point).
* All controllers should have the majority of a CRUD structure (Create, Read, Update, Destroy). This is a checklist for functionality with each entity in your system in that each entity should be creatable, readable (displaying it, can be combined with update), updatable (editable in other words) and destroyable (deletable). Sometimes not all entities will have a delete or create (if they are fixed entities within a table for example) but at least ONE of the CRUD system should be present.
* Models should be named in the singular noun. These usually match the controller names (e.g. if the controller is 'users' the model is 'user'). This is annoying and sometimes confusing but a necessary work around for the MVC system where controllers and models usually have at least a one-to-one relationship (i.e. each controller usually has a corresponding model).
* Views should be created in a nested directory system named after the controller. e.g. if the controller is named 'users' the folder `/applcation/views/users` should exist. All files within that folder should usually correspond to the function name within the controller. So if the controller has a function called `login()` the file `/application/views/users/login.php` should correspond to that view.
* Controller should pull in models and views as needed but models and views should avoid having to rely on other models or views. This point is not always followed but attempts to enforce encapsulation and independence.
* Populate `/application/config/autoload.php` with as _few_ entities as possible. Remember that each entry here gets loaded on _every_ page view.
* We usually use a special library called `site` which lives in `/application/libraries/site.php` this file contains a basic templating system as well as some handy functions which can be called globally.
* A database schema file should be located in `/database/Schema.sql`
	* The schema file should work immutably - i.e. must contain `DROP TABLE IF EXISTS foo;` statements to completely recreate the DB if needed
	* The schema file should contain example INSERT statements where practical to allow another coder to quickly recreate a test environment
	* Since everyone seems to have their own Database setup its usually a good idea to name your desktop/laptop something unique and add a rule for that name in the `/application/config/database.php` file. See an existing project for examples.
* All third party libraries and submodules live in `/lib`. This makes it easy to manage what is part of this project and what are libraries from elsewhere. See the [Package managers](../projects.md) section for more information on 3rd party libraries.
	* If a third party lib is to be used in the project its recommended to make a view inside `/application/views/lib` to load its CSS, JavaScript and HTML. e.g. if there is a 3rd party WYSIWYG editor make a loader for this in `/application/views/lib/wysiwyg.php` which can quickly load all its dependencies.
	* The first place to look for 3rd party libraries is Composer (see [Package managers](../projects.md)) before just cloning a 3rd party Git library into a folder.
* JavaScript files live in `/js`, CSS files live in `/css`.
* Normally a site has a Bootstrap based theme which can expose multiple JS and CSS files these files should *not* be modified (the theme may be updated at some later stage and your changes lost), instead create a file such as `/css/global.css` to override the CSS you may wish to alter aside from the main theme.
* Try to use constants in place of literal strings. For example `SITE_TITLE` is useful to specify whatever the site is currently called. These should live in `/application/config/constants.php`.
* CodeIgniter's provided [session library](http://ellislab.com/codeigniter/user-guide/libraries/sessions.html) is pretty poor and doesn't really serve a purpose. Using the default PHP `$_SESSION` variable is perfectly fine. You will need to add `session_start()` at the bottom of `/application/config/config.php` for new projects to enable this.
* Stick all writable content into `/data`. Examples include things like uploadable pictures or other content. We would recommend making separate sub-folders for each controller such as `/data/foobar/123` (where 'foobar' is the controller and '123' is the DB item that links to it).


MySQL Databases
---------------
> There are only 3 numbers of interest to a computer scientist: 1, 0 and infinity
> - [The Zero One Infinity Rule](https://en.wikipedia.org/wiki/Zero_one_infinity)

Databases are a pain to maintain. They nearly always require installation and sync on installation.
The best way we have found to manage them is to hand code the SQL to create the schema and place it in `/database/Schema.sql`. This file is then usually loaded into a server side MySQL database on load. See an existing project for examples of both this file and a Makefile to load it correctly.

One day we will find a nicer method to manage databases. On that day Satan will have difficulty getting into work due to snow issues.

General tips when creating your database - these are all purely advice and can be ignored as necessary:

* **Casing** - Always lower case, always. Having to hunt though schema files to find if a field is called 'userid', 'UserId', 'UserID', 'userId' or 'userID' will result in death or a Microsoft Certification.
* **Hungarian Notation** - If you don't know what this means: Congratulations! You are either too young or have never worked for Microsoft. Hungarians or their notations will be beaten to death with their own clogs.
* **Seperators** - Use of '_' is recommended for table and field seperators where its not immediately obvious (e.g. 'car_model', 'favourite_color') but can equally be ignored (e.g. 'carmodel', 'favourite_color') depending on preference.
* **Table names** - Are plural nouns (e.g. 'users', 'cars', 'devices', 'locations', 'hair_styles'). Yes this gets annoying because of the English language (e.g. the plural of sheep is sheep, battery is batteries etc.)
* **Primary keys** - Generally its a good idea to use the singular noun table name followed by id with no spacing (e.g. 'userid', 'carid', 'deviceid', 'locationid')
* **Linkage tables** - These are tables that complete a many-to-many relationship. Generally either the 'foo2bar' format or 'foo_to_bar' format are both fine (e.g. 'users2tags', 'users2cars', 'users_to_locations', 'users_to_devices')
* **Indexes** - Learn what `CREATE INDEX` is and [what it does](https://dev.mysql.com/doc/refman/5.0/en/create-index.html). This should follow every `CREATE TABLE` statement to tell the database which fields to index. Any field that has a large number of read filters should be indexed. For example if you use 'users.email' or 'users.username' to identify a user when logging in - index that field! If your application is running slow its usually because you forgot to index something you are reading / filtering by excessively without indexing it.
* **DELETE** - Not so much a database issue, this is usually in the HLL (e.g. CodeIgniter). In 90% of cases a record should never be deleted. Instead add a column to indicate status (e.g. `CREATE TABLE ... status ENUM('active', 'deleted') DEFAULT 'active' ...`). Deleted records cause havoc in later statements and make reporting of historical data impossible. Possible exceptions include linkage table rows and 'temporary' tables such as shopping baskets etc.
* **Varchar / BLOB** - Varchars can have a maximum length of 255. Any content that is likely to exceed this should be created as a BLOB / CBLOB. In MySQL this data type is 'TEXT' (e.g. `CREATE TABLE ... content TEXT...`). TEXT fields cannot be indexed so if you want to lookup by value you should use `VARCHAR(255)` instead - email addresses should always be `email VARCHAR(255)`.
* **Usernames** - Dealing with user logins can be an issue later on if any OAuth is added to the application. We recommend you add a field called `username` to all 'users' tables and index that. Even if your application ONLY accepts email as the login at present copy the contents into this field. Trust us, it makes life easier when the client asks for OAuth via Facebook login or something.
* **User firstnames / lastnames** - You can save yourself a lot of pain and anguish by only asking for the users name (e.g. 'John Smith') rather than a first and last name. Letting the user enter whatever they want is always preferable than forcing the first/lastname convention on them. This is the most frequently bypassed tip so don't feel bad if the user insists on firstname/lastname fields instead.
* **Dates / epocs** - Dates within a database should always be stored as [UNIX epochs](https://en.wikipedia.org/wiki/Unix_epoch). Epochs are a simple integer of the number of seconds since 1970-01-01 00:00. This makes maths on dates extremely simple (e.g. to add a day simply increment by the number of seconds in a day - 60*60*24) and easy to deal with.
* **Refering to dates** - Dates outside of Unix epochs such as human readable dates (e.g. in comments or elsewhere) should be noted in big-endian [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) format. Since we work with a lot of external devs this prevents confusion, it also means named files sort logically (year first, day last). Its also a format non-programmers can pick up without prompting, use it, you'll like it.


PHP / Apache environment setup
------------------------------
> Programming is 1% inspiration, 99% trying to get your environment working.
> - [Hacker News](https://twitter.com/HackerNewsOnion/status/390883204967567360)

For the PHP / CodeIgniter / MySQL development stack you will need to have Apache + PHP running somewhere to actually test what you're developing.

I would suggest Linux if you are familiar with it (and its a simple `sudo apt-get install lamp-server^` to install) or using [XAMPP](https://www.apachefriends.org/index.html) for Windows or Mac.

The following commands pasted into a Bash shell should set everything up on a Debian / Ubuntu based system:

	sudo apt-get install -y lamp-server^
	sudo perl -pi -e 's/^display_errors = .*$/display_errors = On/g' /etc/php5/apache2/php.ini
	sudo perl -pi -e 's/^short_open_tag = .*$/short_open_tag = On/g' /etc/php5/apache2/php.ini
	sudo perl -pi -e 's/^upload_max_filesize = .*$/upload_max_filesize = 32M/g' /etc/php5/apache2/php.ini
	sudo perl -pi -e 's/AllowOverride .+$/AllowOverride all/g' /etc/apache2/sites-available/*default*
	sudo ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load
	sudo service apache2 restart
	echo "Don't forget to update your database information in /application/config/database.php"
	echo "You may also need to point /var/www to where your project lives. The following will set that up:"
	echo
	echo "    sudo rm /var/www -r; sudo ln -s /where/your/project/is /var/www"
	echo


If you want to set up your environment yourself you may find the following tips useful:

* Make sure PHP has `short_open_tags` set to `on` in the php.ini file (XAMPP for some mysterious reason ships without this)
* You may also wish to set `display_errors` to `on` so you actually get errors displayed on screen rather than PHP just returning a blank page and sulking if you make a syntax error
* You will also need a suitable database environment such as MySQL (don't forget to tweak your database settings in `/application/config/database.php` for CodeIgniter projects
* You will need to set `AllowOverride` to `all` in all cases in `/etc/apache2/sites-available/default` to allow Apache to process `.htaccess` files
* You *may* need to enable Apaches `mod_rewrite` depending on the distro
* All our projects assume that the project is installed as the root of the site. We do this to avoid having to figure out where resources are located (as its always easier just to add a prefix `/` at the beginning of all links). This means that you will need to either install the site in Apaches document root *or* clone the repo elsewhere and set `/var/www` as a symbolic link pointing to it. You may find projects like [WWWSet](https://github.com/hash-bang/Bash-WWWSet) helpful to automate this process.


PHP / CodeIgniter project coding style
--------------------------------------
Try to use short tags where possible:

	//Correct & neat
	<?=$foo?>

	// All the following are overly long and complex but are syntactically the same:
	<?php echo $foo; ?>
	// OR
	<? echo $foo ?>
	// OR
	<?php print $foo; ?>


The same goes for loading objects in CodeIgniter/PHP:

	// Correct
	<? $this->load->helper('form') ?>

	// Wrong - Takes up too much room and overly complex
	<?php
	$this->load->helper('form');
	?>


Please use the standard C syntax rather than the alternate PHP syntax:

	// Correct
	<? if ($widgets) { ?>
	<ul>
		<? foreach ($widgets as $widget) { ?>
		<li><?=$widget['name']?></li>
		<? } ?>
	</ul>
	<? } else { ?>
	<div class="alert alert-info">No widgets found</div>
	<? } ?>


	// Wrong (and weird)
	<? if ($widgets): ?>
	<ul>
		<? foreach ($widgets as $widget): ?>
		<li><?=$widget['name']?></li>
		<? endforeach; ?>
	</ul>
	<? elseif: ?>
	<div class="alert alert-info">No widgets found</div>
	<? endif: ?>


**[Back to Table of Contents](../README.md)**
