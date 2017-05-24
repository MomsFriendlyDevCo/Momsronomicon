NPM Module Writing Guide
========================
Below are some general notes about writing NPM modules.

1. Create the basic structure of your application. This should include at least:
	* [package.json](http://browsenpm.org/package.json)
	* [LICENCE](https://choosealicense.com/) (when in doubt just use an [MIT license](https://choosealicense.com/licenses/mit/))
	* [.gitignore](https://www.gitignore.io) (generally just a file with a line of `node_modules/` is enough)

2. Place all source files into `./src`

3. Use a compile step via [gulp](https://github.com/MomsFriendlyDevCo/vote-tally/blob/master/gulpfile.js) to produce ES5 safe + miinified versions of your JavaScript + CSS files


FIXME


Common Gotchas
---------------

1. For reasons of stupidity GitHub pages runs everything via Jekyl whether you want it to or not. If you find that your `node_modules` directory is not being served make sure there is a `config.yml` file in the root of the `gh-pages` branch containing the one-line content: `exclude: []`




**[Back to Table of Contents](../README.md)**
