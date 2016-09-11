Projects
========
> Programs are meant to be read by humans and only incidentally for computers to execute
> - H. Abelson and G. Sussman (Structure and Interpretation of Computer Programs)

Each project should include at least a `README.md` file to describe the project either with instructions on how to install it _or_ a Makefile / Grunt / Vagrant config file to do the installation on their behalf.

Unbreakable rules with projects:

* All projects should work out-of-the-box as far as possible. Excepting databases (which _always_ need installing and fiddling with) your project should work immediately after `git clone`. Failure to follow this rule will result in damnation and/or Matt killing you.
* Database schemas should be *human readable* - Do not just dump `mysqldump` / `mongodump` into a file. It should be readable and less than 1mb (don't dump a terabyte of SQL into a file and call it good). Failure to follow this rule will result in Matt killing all your pets (if you do not have any pets, Matt will by you some then kill them over your keyboard).
* You may see folds in existing code these resemble three opening or closing braces e.g. `Some code {{{ ... }}}`. These are flags to a text editor that the text between the braces should be grouped with a labeling comment. This is helpful to gather large related blocks of code together and make the source code more readable.


Package managers
----------------
There are quite a few package managers out there. We've found that the following work quite well:

* **[Bower](http://bower.io)** - This is probably the package manager that will get the most use. Its centered specifically on front-end code (mainly JavaScript and CSS) and works fine with any project.
* **[Composer](http://getcomposer.org)** - A package manager specifically for PHP, this provides a nice simple Object Orientated interface that takes advantage of PHP's Magic loading (i.e. `$foo = new BarObject()` will magically load whatever files `BarObject` lives in).
* **[NPM](https://www.npmjs.org)** - Used usually for backend JavaScript / NodeJS dev only.
* **Everything else** - As previously stated, dump everything else in `/lib` so everyone at least knows its an external component.

All three package managers dump their files in their own folders (`/bower_components` for Bower, `/vendor` for Composer and `/node_modules` for NPM). Composer and NPM also update their own config files (`/composer.json` and `/package.json` respectively).

All files (config files and downloaded files for each submodule) should be included within Git. For example if you install Bootstrap via bower (i.e. `bower install bootstrap`) the created folder (`/bower_components/bootstrap`) should be committed into Git on your next push. The principle here is that someone cloning your project from scratch should be able to get your project running _without_  needing to re-run the package manager to pull in all the prerequisites (e.g. `bower install`, `npm install`, `composer install` on each pull).

An exception to the above can be made for open-source components (not full projects). For example a widget that belongs in its own Git repo may omit any pre-requisite packages as the package manager will download and install these within the parent project anyway.


**[Back to Table of Contents](README.md)**
