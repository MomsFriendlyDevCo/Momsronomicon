Angular projects
================
When we refer to 'Frontend JavaScript' we usually mean [AngularJS](http://angularjs.org), although there can also be a bit of [jQuery](http://jquery.com) thrown in to do some of the more complex DOM manipulation.

Frontend coding style
---------------------
Most of the same JavaScript styles under the [NodeJS coding section](style-node.js) are also applicable to Angular / Frontend JavaScript. The below is specific to Angular projects.

Miscellaneous stuff you might not know about AngularJS:

* [Ternarys](https://en.wikipedia.org/wiki/%3F:) are an easy way of wrapping an if...then...else block inside an Angular expression. For example `Hello {{user.name ? user.name : 'Anonymous'}}` outputs the user name if there is one otherwise it uses the string 'Anonymous'. This style can be used in any Angular expression including ng-class e.g. `<i class="fa" ng-class="ok ? 'fa-check-circle' : 'fa-exclamation-circle'"/>` changes the icon depending on the value of `$scope.ok`.

* `ng-options` is a pain to use and everyone screws up the syntax. We generally just use a `<option ng-repeat="item in items"/>` repeater instead as this gives you far more control.

* When creating blank projects always ensure you have an outer global controller (i.e. the body element should be declared `<body ng-app="app" ng-controller="globalController">`. This gives you a single nestable controller that all others will inherit from. Storing things like logged in user information in its scope will allow access from any other controller.

* When pulling in data via an Angular model *do not* add change the data or add custom values here. Setup a `$scope.$watch` [watcher](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) instead. This will apply an operation when *anything* writes to the incoming data automatically.

* `ng-show` and `ng-enabled` have opposite directives using `ng-hide` and `ng-disabled`.


Optimization techniques
-----------------------
Angular has a few techniques which allow the frontend code to run much quicker than default:

* Set `$compileProvider.debugInfoEnabled(false)` to disable the 'helpful' extra CSS styles such as `ng-binding` from being added. Automate this in the intial config with something like the solution [posted here](https://gist.github.com/capaj/d15a53395c73f545b362)

* `{{::foo}}` will template 'foo' exactly once and never update it again - this makes the DOM lightning fast if you only want Angular to insert the value of a variable once.

* Adding `track by` to `ng-repeat` elements hugely speeds up DOM refreshes when using repeats e.g. `<div ng-repeat="user in users track by user._id"></div>`. ngRepeats normal behaviour is to remove all elements and re-insert on an array change, using `track by` allows inserts and removals of elements but leaves existing DOM elements alone - preventing costly DOM removal/reinsert behaviour.

* The difference between `ng-show` and `ng-if` is that `ng-show` will only HIDE an item but all of its child Angular directives will still execute. `ng-if` removes the item from the DOM all together. `ng-if` is top-down in processing order, `ng-show` is bottom-up. While the temptation is to see `ng-if` as better - since it saves CPU by not having to redraw its child items - it has a major performance penalty in adding and removing from the DOM. The general rule is - if the display of an item is unlikely to change much OR has child Angular directives use `ng-if`, otherwise use `ng-show`.


Project layout
--------------
After experimenting with a variety of different project layouts we have found that the following works quite well for AngularJS projects:

The project tree breakdown is listed below. For each path an 'edit chance' is given (i.e. the possibility of the developer needing to change the contents of that directory) and a brief description.

| Path                                                | Edit chance | Description                   |
|-----------------------------------------------------|:-----------:| ------------------------------|
| `/`                                                 | Rare        | Root project directory        |
| `/app/`                                             | Common      | Root Angular directory        |
| `/app/app.js`                                       | Rare        | Main Angular initializer file |
| `/app/routes.js`                                    | Common[1]   | Main Angular initializer file |
| `/app/controllers/`                                 | Common      | Angular controller directory  |
| `/app/controllers/global.js`                        | Common[2]   | Angular rootScope controller  |
| `/app/directives/`                                  | Common      | Angular directives directory  |
| `/app/filters/`                                     | Common      | Angular filters directory     |
| `/app/models/`                                      | Common      | Angular models directory      |

The above is sometimes subject to change depending on the backend environment or project layout. Sometimes the `/app` directory can be stored as `/js/app` or elsewhere in the file tree. As much as possible the inside of that directory should resemble the above layout though.

Notes:

1. Only applies if using the Angular [UI-Router](https://github.com/angular-ui/ui-router) module.
2. The Angular rootScope controller should be attached to the same element as the ng-app directive. e.g. `<body ng-app="app" ng-controller="globalController"></body>`.


Further reading
---------------
The following external references are recommended:

* [Angular Style Guide](https://github.com/johnpapa/angular-styleguide)
* [ES6 Arrow Syntax](http://shivganesh.com/2015/08/es6-arrows/) - Some simple effective examples of ES6 arrow syntax


External resources
------------------
We find we use the following Angular modules a in most projects:

* [angular-resource](https://docs.angularjs.org/api/ngResource)
* [angular-ui-router](http://angular-ui.github.io/ui-router/site)
* [angular-xenophilous](https://github.com/hash-bang/ng-xenophilous)
* [ng-mfdc](http://momsfriendlydevco.github.io/ng-mfdc) - Various Angular directives in use at MFDC


**[Back to Table of Contents](../index.md)**