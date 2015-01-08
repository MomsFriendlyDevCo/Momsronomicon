Angular projects
================
When we refer to 'Frontend JavaScript' we usually mean [AngularJS](http://angularjs.org), although there can also be a bit of [jQuery](http://jquery.com) thrown in to do some of the more complex DOM manipulation.

Frontend coding style
---------------------
Most of the same JavaScript styles under the [NodeJS backend chapter](#javascript-coding-style) are also applicable to Angular / Frontend JavaScript. The below is specific to Angular projects.

Miscellaneous stuff you might not know about AngularJS:

* `{{::foo}}` will template 'foo' exactly once and never update it again - this makes the DOM lightning fast if you only want Angular to insert the value of a variable once.
* Adding `track by` to `ng-repeat` elements hugely speeds up DOM refreshes when using repeats e.g. `<div ng-repeat="user in users track by user._id"></div>`. ngRepeats normal behaviour is to remove all elements and re-insert on an array change, using `track by` allows inserts and removals of elements but leaves existing DOM elements alone - preventing costly DOM removal/reinsert behaviour.


Project layout
--------------
After experimenting with a variety of different project layouts we have found that the following works quite well for AngularJS projects:

The project tree breakdown is listed below. For each path an 'edit chance' is given (i.e. the possibility of the developer needing to change the contents of that directory) and a brief description.

| Path                                                | Edit chance | Description |
|-----------------------------------------------------|:-----------:| ------------|
| `/`                                                 | Rare        | Root project directory |
| `/app/`                                             | Common      | Root Angular directory |
| `/app/app.js`                                       | Rare        | Main Angular initializer file |
| `/app/routes.js`                                    | Common[1]   | Main Angular initializer file |
| `/app/controllers/`                                 | Common      | Angular controller directory |
| `/app/controllers/global.js`                        | Common[2]   | Angular rootScope controller |
| `/app/directives/`                                  | Common      | Angular directives directory |
| `/app/filters/`                                     | Common      | Angular filters directory |
| `/app/models/`                                      | Common      | Angular models directory |

The above is sometimes subject to change depending on the backend environment or project layout. Sometimes the `/app` directory can be stored as `/js/app` or elsewhere in the file tree. As much as possible the inside of that directory should resemble the above layout though.

Notes:

1. Only applies if using the Angular [ngRoute](https://github.com/angular/bower-angular-route) module.
2. The Angular rootScope controller should be attached to the same element as the ng-app directive. e.g. `<body ng-app="app" ng-controller="globalController"></body>`.


**[Back to Table of Contents](README.md)**
