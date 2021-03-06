Px Component Generator
===============

## Introduction

The Px Component Generator is a starting point for building your own Predix UI Component. There are several technologies that we use to make working with components easier and to aid in automating builds.
Familiarize yourself with these tools (which we cover in the Technologies section further down the page) so your component can look and feel like everything else in the Predix UI ecosystem.  The Predix UI Component
Generator relies on [Yeoman](http://yeoman.io).

## Yeoman & Yeoman Generator

A generator is something run by [Yeoman](http://yeoman.io) to scaffold a software application, in this case a Predix UI component.  Yeoman
 is an application environment for writing and running generators. Yeoman lives in the [npm](https://npmjs.org) package repository when installed globally (-g).

```
$ npm install -g yo
```

_Note: This generator works in yo 1.2 and above. To find the version of yo on your system, type `$ npm list -g yo`_

You can think of a generator like a plug-in. `generator-px-comp` is a generator that scaffolds a Predix UI component

To install the Predix UI Component generator locally, run:

```
$ git clone https://github.com/PredixDev/generator-px-comp #grab the generator.
$ cd generator-px-comp #go into the generator folder.
$ npm link #this command create a global link on your machine for the px-comp generator.
```

Finally, initiate the generator from an empty directory to scaffold your new Predix UI component:

```
$ cd .. #cd up and out somewhere...anywhere outside the generator
$ mkdir px-something
$ cd px-something
$ yo px-comp
```

Running `yo px-comp` will ask you a few questions and then scaffold a sample component, which includes gulpfile.js, package.json, bower.json, tests, etc in your directory.

Once you have a sample Predix UI component, you can...

```
//build css
$ gulp sass

//start a local server
$ gulp serve

//nav in a browser to
localhost:8080
```

`gulp sass` compiles [Sass](http://sass-lang.com/) into CSS.

`gulp serve` starts a HTTP server that enables correct finding of bower dependencies for local runs. It also runs [Browsersync](https://www.browsersync.io/) to automatically rebuild sass and reload the current page when a change occurs.

After you've verified the component works, edit the sample Predix UI component, tests and dependencies that were scaffolded.

When your component is finished, update your HISTORY.md file, commit everything in Git and tag an initial release.

## Structure

It might seem like the generator creates quite a lot of files. Don't worry, most of them are packaged dependencies that aren't part of your Predix UI Component itself (i.e. the `node_modules` and `bower_components` directory).
The files that are part of the Px component are:

- **package.json** — An [npm](https://npmjs.org/) package file for specifying information and dependencies.
- **.travis.yml** - A build file for the [travis CI](https://travis-ci.org/) testing platform.
- **gulpfile.js** — A build file for the [gulp](http://gulpjs.com/) task runner.
- **bower.json** — A [Bower](http://bower.io/) package file for specifying information and dependencies.
- **.bowerrc** - A configuration file for bower.
- **editorconfig** - A configuration file for your editor, with preconfigured recommended settings you can change according to your own specifications.
- **.gitignore** - A file which tells git which files to **not** commit.
- **.jshintrc** — [JSHint](http://www.jshint.com/) configuration file for managing JavaScript code quality.
- **<COMPONENT>.html — This is the file you'll be building your component in.
- **sass/** — All styles should go here. This folder contains [Sass](http://sass-lang.com/) stylesheets for 'sketch', 'predix' and 'demo' styles. The 'predix' styles import 'sketch' and build upon them. The 'demo' styles are used i n your demo page.
- **css/** - A folder with pre-compiled, minified CSS files. These files should NOT be edited - see Sass files above.
- **index.html** - A demo page which imports your component and calls the documentation builder, as well as demos off your component.
- **test/** — All functional tests for the px-component go here.
- **.github/PULL_REQUEST_TEMPLATE.md** - A pull request template used by Github.
- **.github/ISSUES_TEMPLATE.md** - An issue template used by Github.
- **CONTRIBUTING.md** - the Predix UI Team Contribution guide.
- **HISTORY.md** - A file that contains your version history.
- **LICENSE.md** - A license file.
- **wct.conf.js** - A configuration file for [Web Component Tester](https://github.com/Polymer/web-component-tester).
- **README.md** — A starter readme file in the Markdown format.

## Requirements

A component **must** meet the following requirements to be considered part of the Predix UI ecosystem:

- Must provide a README
- Must provide an email address for support requests
- Must provide passing tests in the test folder
- Must provide Sass that compiles down to regular CSS


## Tool Chain Reference

### npm

[npm](https://npmjs.org/) is a package manger for Node.js. We rely heavily on npm to install our gulp tasks, and also to install some of our tools like Bower and gulp itself. If you've installed Node.js then npm should already be available on your system. Be sure to familiarize yourself with npm first and foremost as it is used throughout the component/Predix landscape.

### Gulp

We use [gulp](http://gulpjs.com/) to build all of our components and Design Extensions. Take some time to familiarize yourself with the [gulp documentation.](http://gulpjs.com/)

The Component Seed comes with two built in gulp tasks: `gulp serve` and simply `gulp`. The default `gulp` task will clean, build css and a [Polymer style module](https://www.polymer-project.org/1.0/docs/devguide/styling) from the .scss files in the `/sass` folder. The `gulp serve` task will start up a http server to serve up your documentation/demo pages as well as [Browsersync](https://www.browsersync.io/) to automatically reload the page as HTML changes as well as recompile sass into css (and reload the current page) as it changes.

### Bower

[Bower](http://bower.io) is a package manager for the web, primarily focused on front-end JavaScript. We use bower to install all of our component dependencies and we would strongly encourage you to do the same. By using bower, teams are able to easily add your component to their project and update it as it is improved. Bower removes the need for a lot of manual copy/paste work which can lead to errors and generally eats up time.

### Sass

We request that all components provide their styles in [Sass](http://sass-lang.com/) format. This allows us to better leverage variables for color palettes, typography, etc. In this way components can have a consistent look and feel across all Px components. It also ensures that they have a known API to program against and they're not inventing things which won't work in
all systems.

By default the task will attempt to compile all Sass files in the `sass/` folder to individual stylesheets.


### RECOMMENDED READING

[Inuit CSS](https://github.com/inuitcss/getting-started) - Scalable and Modular Architecture for CSS

[Javascript the Good Parts](http://shop.oreilly.com/product/9780596517748.do) - Insights into Javascript by Douglas Crockford

---

## FAQ

### What does the tilde "~" mean in the version numbers?

The tilde is used to specify a version range. `~1.9.1` translates to "any version greater than or equal to 1.9.1 but less than 1.10.0".

Bower uses [Semantic Versioning (aka semver)](http://semver.org/) just like npm. [Here's a great explanation of all the ways you can specify version ranges in semver.](https://npmjs.org/doc/json.html#dependencies) Any component in the Design Extension ecosystem **must** use semantic versioning, otherwise tools like bower will be unable to consume it.


### I made changes to a component but bower keeps pulling down the old code

There are two things that can be going wrong in this situation.

1. You made code changes but you didn't create a new tag (Solution: create and push a new tag - See below.).
2. You replaced an existing tag but didn't clear your bower cache (Solution: run a *bower cache clean* command in your terminal - See below.).


#### You made code changes but you didn't create a new tag

Bower works off of tags, so if you add code to your component you have to version up the tag. This is why [semver](http://semver.org/) is so important. You want all those version numbers to mean something. If you haven't created a new tag **and pushed it to the remote server** then you won't see any changes.

To create a local tag:
``` bash
$ git tag v0.1.0
```

To push your local tags to your remote:
``` bash
$ git push origin --tags
```

To delete a local tag:
``` bash
$ git tag -d v0.1.0
```

To delete a tag on your remote:
``` bash
# WARNING! Make sure no one is using the tag! This is NOT recommended.
$ git push origin :/refs/tags/v0.1.0
```

#### You replaced an existing tag but didn't clear your bower cache

Perhaps you tagged something that was broken and needed to delete the tag locally and on your remote using the steps outlined above. Even after you've done this bower is still holding a cached instance of your library at the previous, bad tag. To tell bower to clear its cache use:

``` bash
# Will clear everything in bower's cache
$ bower cache clean

# Will just clear the cache of your component
$ bower cache clean <component>
```
After you've cleaned the cache it might also be a good idea to delete that component's folder from the `bower_components` directory. Then you can try to run `bower install` again.

## Running on an existing component

The `px-comp` has a "sub-generator" in it to scaffold tests - `px-comp:test-gen`. this sub-generator is also run when the full px-comp generator is run.

You may run the sub-generator individually on existing components that doesn't already have tests:

```
$ cd my-existing-component
$ yo px-comp:test-gen <COMPONENT>
```

Sample tests will be generated in the test folder. You'll need to edit the sample tests and add your own test to the base tests. Add your tests inside the COMPONENT-custom-tests.js file.  If you already have existing tests specified in wct.conf.js, make sure not to overwrite the file, and add the new tests manually under the suites array in wct.conf.js.
