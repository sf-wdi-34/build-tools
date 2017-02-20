<!--
Creator:
Last updated by: Brianna
Market:
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Build Tools

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

Build Tools are software that allows us to speed up and automate our work, including compiling our code, minification, concatenation, server automatic browser reloading, and other tasks.  They are a commonly-used part of React development workflow.

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

* Explain roles of build tools: minification, compilation, concatenation/bundling, compression, file watching, etc.
* Compare build tools: Rake, Gulp, Webpack.
* Use build tools to automate workflow.


### Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

* Write client-side applications with JavaScript and CSS.

## What are Gulp and Webpack?

* These are build tools. Each is commonly used with React to compile JavaScript code and/or manage other assets.
*  You can think of this like the asset pipeline in Rails. Today, we'll look at ways to accomplish tasks like these when we're not working with Ruby or Rails.


## Review

<details>
<summary>
Q. What is minified code, and why do we minify code?</summary>

Code in which all unnecessary characters have been removed from source code without changing its functionality at all. It allows for a faster response and significantly reduces the size of the code, requiring less bandwidth.

<br>
<br>
</details>


<details>
<summary>
Q. When have you seen minified code before?</summary>

CDNs for JavaScript tools like jQuery and Angular.

<br>
<br>
</details>


<details>
<summary>
Q. What does it mean to compile code? What compiled languages have you heard of, and what languages do they compile to?</summary>


Compiling code (sometimes called preprocessing) is taking a file written in one language, like SASS, and running a special "compiler" program to convert it into a new file written in the language we want. For the browser, we can compile SASS into CSS and CoffeeScript into JavaScript.

<br>
<br>
</details>


<details>
<summary>
Q. What tool did we use in Rails to help concatenate and minify our JS and CSS? Why do we want concatenation?</summary>

Rails Asset Pipeline, which helped to concatenate all JS and CSS files into one, allowing us to speed up our application and serving of static files.

<br>
<br>
</details>

<br>

In summary, build tools help us complete tasks like compiling and minifying code so we don't have to do those things manually and repeatedly.

We are going to briefly touch on two popular options for build tools: Gulp and Webpack.

## Gulp

<img src="gulp.jpg" width="54px">[Gulp Documentation](http://gulpjs.com/)
<img src="gulp.jpg" width="54px">

Gulp is an popular open-source automation tool built on Node.js that runs tasks to manipulate files in your application.

With its tasks, Gulp is similar to `rake` in Ruby.

Rake is used to help automate a bunch of tasks for us when building Rails applications. In Rails 5, most of `rake`'s jobs are available through the `rails` command for convenience.

Here are examples of these `rake` tasks:

```
$ rake db:migrate
$ rake assets:precompile
```


## Gulp Example

Fork and clone this ["Gulp Bamsay" repo](https://github.com/ga-wdi-exercises/gulp-bamsay). During this workshop, we'll practice making gulp tasks, create tasks to lint code with `jshint` and to compile SASS, and make a combined task that runs automatically when files change.

### Installing Gulp

**Goal**: install Gulp.

To install globally on your computer:
```bash
$ npm install gulp -g
```

To install as dependency in one node project:
```bash
$ npm install gulp --save-dev
```

>Note: writing `--save-dev` instead of `--save` adds a separate  `"devDependencies"` object in `package.json`.  Don't worry too much about the difference for now; just know these plugins would be used differently in production!

1. Install the `gulp` command globally.

1. Install `gulp` as a dependency of the Gulp Bamsay project.

1. Create a file called `gulpfile.js` in the project's root directory. This will contain task configuration.

1. Run `gulp` in Terminal.

  <details><summary>click for sample output</summary>
  ```bash

  [10:36:31] Using gulpfile ~/GeneralAssembly/WDI/build-tools/gulp-example/gulpfile.js
  [10:36:32] Task 'default' is not in your gulpfile
  [10:36:32] Please check the documentation for proper gulpfile formatting
  ```
  </details>

1. Read the error message carefully and guess what you need to do next.

### Gulp Tasks

**Goal**: Create a Gulp task.

1. <details><summary>Research: what is a Gulp task?</summary>

  In Gulp, we create tasks that can transform our code. `gulp.task` is a method which we use to define our tasks. Its arguments are the task name, it's dependencies and callback function.
  </details>

1. The `gulp` package is already included in the Gulp Bamsay project.  Inside `gulpfile.js`, `require` the `gulp` module and save the package's exports as a variable.  This will allow us to call upon Gulp to create a task.

  <details><summary>click for code</summary>
  ```js
  // gulpfile.js
  var gulp = require('gulp');
  ```
  </details>

#### A First Task

By default, the `gulp` terminal command checks your `gulpfile` for a `default` task.

1. Define your first task as this `default` task, in `gulpfile.js`:

  ```js
  // gulpfile.js
  var gulp = require('gulp');

  // define a task with the name of 'default'
  // the function is a callback to perform when the task is run
  gulp.task('default', function() {
    console.log('I am the default task!');
  });
  ```

1. In your terminal, try running `gulp` again.

  >Now, Gulp should be able to find the default task in your `gulpfile.js`. It will then execute the callback that you define for your task.

  You should see something like the following:

  ```bash
  [10:37:37] Using gulpfile ~/GeneralAssembly/WDI/build-tools/gulp-example/gulpfile.js
  [10:37:37] Starting 'default'...
  I am the default task!
  [10:37:37] Finished 'default' after 104 μs
  ```

1. <details><summary>We used the string `'default'` to name the task. Do you think it matters what we call this task?</summary>

  Yes, and no. While you can certainly change `default` to `wombat`, it would not be very descriptive of the task.

  Also, for whatever you define 'name' as in your task (`gulp.task('name', callbackFunction)`), you run the task by runnign the following in the command line:

  `$ gulp <name>`

  The name `default` is special in Gulp, though. If our task's name is `default`, we can just run `$ gulp`.

  </details>


#### Write your own Gulp task

**Goal**: practice writing Gulp tasks.

1. Write a task that will `console.log` the current date/timestamp when it is run.

[check an example solution](https://github.com/ga-wdi-lessons/build-tools/blob/joe_updates/gulpDateTask.js)

### Gulp Plugins

In addition to letting us write our own tasks completely from scratch, Gulp has many [plugins](http://gulpjs.com/plugins/) that we can use in our applications.

#### Installing a Gulp Plugin

To install a Gulp plugin:
- install the plugin package individually using `npm install <dependency-name> --save-dev`.
- `require` the plugin in the `gulpfile`.


#### Jshint Plugin

**Goal**: Install `jshint` plugins to easily identify JavaScript errors.  If stuck, see [example solution code](https://github.com/ga-wdi-exercises/gulp-bamsay/tree/jshint-solution).

1. Install the node packages plugins `jshint`, `gulp-jshint`, and `jshint-stylish` for your project.

  <details><summary>click for code</summary>
  ```bash
  $ npm install jshint gulp-jshint jshint-stylish --save-dev
  ```
  </details>

1. `require` `gulp-jshint` and `jshint-stylish` in the `gulpfile`.

  <details><summary>click for code</summary>
  ```js
  // gulpfile.js
  var gulp = require('gulp');
  var jshint = require('gulp-jshint');
  var stylish = require('jshint-stylish');
  ```
  </details>

1. We're about to add a Gulp task called `jshint` (though we could call it `lint` or another name).  Examine the code below.

  ```js
  // gulpfile.js
  // ...
  gulp.task('jshint', function() {
    return gulp.src('./js/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter(stylish));
  });
  ```

1. <details><summary>Research: what is `gulp.src`?</summary>
  `gulp.src` specifies file source paths. It can also take an array of source paths.
  </details>


1. <details><summary>Research/review: what does `'./js/*.js'` represents?</summary>

  The `*` is looking for any file ending in `.js` in the specified directory, which is `./js/`. Essentially, it's setting us up to run the next few lines of code on all JavaScript files in the `js` directory.
  </details>

1. <details><summary>Research: what is the `.pipe()` method doing in the snippet above?</summary>

  `.pipe()` is used to pipe (send) the source file/files into a plugin. These pipes can chain tasks together, so you can add as many dependencies as you need!

1. Add the previous task definition to the `gulpfile`, then run the `jshint` gulp task in your command line (`gulp jshint`).

1. <details><summary>Research: What is the `jshint` method doing in the snippet above?</summary>

  `jshint` is a linter; it detects errors or styleguide violations in our code.
  </details>

>Note: Instead of calling this task `jshint`, we could have added this as our `default` task. Then, we would simply run `$ gulp` instead.

Here's  commented code for this task:

```js
// gulpfile.js
var gulp = require('gulp');
var jshint = require('gulp-jshint');
var stylish = require('jshint-stylish');

gulp.task('jshint', function() {      // register jshint task
  return gulp.src('./js/*.js')        // load all .js files in ./js/
  .pipe(jshint())                     // run jshint (from package) on the files
  .pipe(jshint.reporter(stylish));    // report jshint output in a stylish way
});
```

#### Gulp SASS Plugin

**Goal**: use Gulp to compile our SASS code into CSS.

We are going to be using the following `gulp-sass` plugin: [Gulp-Sass](https://www.npmjs.com/package/gulp-sass).

Continue along on the same `gulpfile.js`. Free to copy the code above if needed.

1. Install the `gulp-sass` package for the Gulp Bamsay project, and save it as a development dependency.

  <details><summary>click for code</summary>
  ```bash
  $ npm install gulp-sass --save-dev

  ```
  </details>

1. Require the `gulp-sass` dependency in your `gulpfile`. For example, `var sass = require("gulp-sass");`.

1. Next, we'll add a new task. First, examine the code below.

  ```js
  gulp.task('sass', function () {
   return gulp.src('./css/**/*.scss')
     .pipe(sass().on('error', sass.logError))
     .pipe(gulp.dest('./css/'))
  });
  ```

1. <details><summary>Research: what files are selected with `gulp.src`?</summary>

  All the `.scss` files inside any directory that is inside the `./css/` directory.

  </details>

1. <details><summary>Research: what does the line with `sass.logError` do?</summary>

  It will log any SASS errors.
  </details>

1. <details><summary>Research: what does the `gulp.dest()` line do?</summary>

  It will copy our results to a given directory. In this case, to our `css` directory.
  </details>

1. Add the task to your `gulpfile`, and then run `gulp sass` from Terminal.

1. If the task runs successfully, you should see that `css/styles.css` has been updated (check with `git status`).


How is that helpful to our workflow? While Gulp does a great job of executing these types of tasks one at a time, it becomes extremely powerful when we start to compose different tasks together.

### Gulp Watch and Connect

We are going to add two more dependencies to help automate these tasks further.  Our goal is to see any SASS changes reflected immediately without manually reloading the server or refreshing our browser. We can also run tasks one after the other automatically to make the process faster during development.

The two new dependencies are [Gulp Watch](https://www.npmjs.com/package/gulp-watch) and [Gulp Connect](https://www.npmjs.com/package/gulp-connect).


1. Install `gulp-watch` and `gulp-connect` as development dependencies, and `require` them in the `gulpfile`.

1. Add two new tasks, and examine their code:

  ```js
  gulp.task('watch', function () {
   gulp.watch('./css/**/*.scss', ['sass']);
  });

  ```

  ```js
  gulp.task('connect', function() {
    connect.server({ livereload: true });
  });

  ```

1. <details><summary>Research: what is `gulp.watch()` doing?</summary>
  It's a method that checks to see if a file was saved.  It's "watching" our `.scss` files for changes, and it is running a list of tasks (just `['sass']`) whenever the files change.
  </details>

1. <details><summary>Research: what is `connect.server({livereload: true})` doing?</summary>

  This lets the web server reload complied files and refresh the browser automatically.
  </details>

1. Run `gulp watch` in your Terminal, and leave it running. If you haven't yet, open `index.html` in your browser.  

1. Make a change to `css/styles.scss`, then check your Terminal and your browser again.  Refresh the page in the browser to see the new style changes.

1. We shouldn't have to reload the page manually. `gulp-connect` can help.  Add `.pipe(connect.reload())` to the `sass` task:

  ```js
  gulp.task('sass', function () {
   return gulp.src('./css/**/*.scss')
     .pipe(sass().on('error', sass.logError))
     .pipe(gulp.dest('./css/'))
     .pipe(connect.reload());
  });
  ```

1. Add the following at the bottom of `gulpfile.js` to create a `default` task that runs the three others:

  ```js
  // gulpfile.js
  gulp.task('default', ['sass', 'connect', 'watch']);
  ```

1. Run `gulp` in terminal.

1. <details><summary>Why don't we need to specify our task name(s) in the above command?</summary>

  We used `default` as the name of the new task that runs three other tasks.  Gulp will automatically execute the `default` command.
  </details>


  You should see output like below:

  ```
  [13:25:59] Using gulpfile ~/GeneralAssembly/WDI/build-tools/gulp-example/gulpfile.js
  [13:25:59] Starting 'sass'...
  [13:25:59] Starting 'connect'...
  [13:25:59] Finished 'connect' after 18 ms
  [13:25:59] Starting 'watch'...
  [13:25:59] Finished 'watch' after 15 ms
  [13:25:59] Server started http://localhost:8080
  [13:25:59] LiveReload started on port 35729
  [13:25:59] Finished 'sass' after 72 ms
  [13:25:59] Starting 'default'...
  [13:25:59] Finished 'default' after 3.63 μs

  ```

1. Instead of looking at `index.html` as a file, go to `localhost:8080` in your browser.  Try changing the SASS code, and see what happens!

1. Add and commit your changes to save your progress.


## Webpack

[Webpack Documentation](https://webpack.github.io/)

Webpack is known as a "module builder," or a bundler.  It is used to bundle JavaScript files to run in our browsers, and can be used for transforming, bundling, or packaging assets and resources. In essence, it returns a brand new version of your code.  Webpack can alleviate large file sizes somewhat by compiling and bundling the code together.

Task runners like Gulp need to rebuild the entire application every time you save. Webpack only rebuilds the modules you have specifically edited!

### Install Webpack

**Goal:** Install Webpack.

1. Switch to the `webpack_starter` branch in the Gulp Bamsay project.

1. Install webpack globally with `npm install -g webpack`, and install it as a development dependency for Gulp Bamsay with  `npm install webpack --save-dev`.

  > Note: Webpack 2 came out in February 2017. It added exciting features like ES6 support. We're going to stick with webpack 1, which will require adding an extra tool called `babel`.

1. Run `webpack` in Terminal.

  You should see output like this:

  ```bash
  webpack 1.14.0
  Usage: https://webpack.github.io/docs/cli.html

  Options:
    --help, -h, -?
    --config
    --context
    --entry
  ...
    --display-cached-assets
    --display-reasons, --verbose, -v

  Output filename not configured.
  ```

1. <details><summary>What does this tell us?</summary>

  We must be missing some configuration. Webpack needs an output filename.
  </details>

### Configure Webpack

**Goal**: Configure Webpack.

1. Create a new file in the root directory of the project: `webpack.config.js`

  This file will define the folders and files that we want bundled, where we want the bundled files to end up, and any other functionality we want from webpack.

1. In `webpack.config.js`, add the following code:

  ```js
  var path = require('path');
  ```

1. <details><summary>What do you think this code is doing?</summary>

  This requires `path`, a built-in Node.js package for handling file paths.
  </details>

1. Set up a `module.exports` object for the `webpack.config.js` module you're creating in this file:

  ```js
  module.exports = {
    // Entry accepts a path or paths in various formats.
    // We're using an object, which is convenient with complex configurations.
    entry: [
      path.join(__dirname, 'js')
    ],
    output: {
      path: path.join(__dirname, 'build'), // often called 'dist'
      filename: 'bundle.js'
    }
  };
  ```  

1. <details><summary>What do you think this section does?</summary>

  Here we are defining the entry point of our webpack. In other words, what directory do we want to look into and bundle? We're also saying which directory the output should go into (in this case, `build`) and what the output file name should be.

  </details>

1. Try running `webpack` in your terminal again. What happens?  Check out your `build` folder, and see that the `bundle.js` file was created.

### Set Up Webpack Server

**Goal**: Use webpack to serve the site's `index.html` through `js/index.js`.

1. Install `webpack-dev-server` as a development depencency in the Gulp Bamsay project. Since we're using webpack version 1, install `webpack-dev-server` at version 1.16.3.

  <details><summary>click for code</summary>
  ```bash
  $ npm install --save-dev webpack-dev-server@1.9.0
  ```
  </details>

1. For convenience, add the following into `package.json`'s `scripts` object:

  `"start": "webpack-dev-server --content-base build"`

1. Run `npm start` in your terminal. You should see output that looks like the image below, and your Terminal tab should continue to run a `node` process.

  ![npm Start](npmStart.png)

1. If you open your browser to `localhost:8080`, you should see a simple `index.html` rendered through your `js/index.js` file.

1. Try making a change to `index.html`. What happens in the browser? What if you refresh?

### Configure Web Server

**Goal**: Add some configuration options for the server.  

1. Inside `module.exports` from `webpack.config.js`, add the code below. Once you have that change, remove ` --content-base build` from the `start` script in your `package.json`. Run `webpack` again to ensure your server still works the same way.

  ```js
  // webpack.config.js
  // inside module.exports
  devServer: {
    contentBase: path.join(__dirname, 'build')
  }
  ```

1. In the same `devServer` object, set up the server to parse the host and port from environment variables so this is easy to customize.

  ```js
  host: process.env.HOST,
  port: process.env.PORT
  ```

1. In the same `devServer` object, enable history API fallback routing works based on the HTML5 History API. This is a good default that will come in handy in more complicated setups.

  ```js
  historyApiFallback: true
  ```

1. In the same `devServer` object, include the following code to automatically add the `webpack-dev-server` client entry point to the webpack configuration: `inline: true`.  Run `webpack` again to see what changed.


### Hot Module Replacement

**Goal**: avoid having to run `webpack` when we change code.

Having to run `webpack` every time you make a change will get repetitive quickly. We can change up the `webpack-dev-server` to help us out.

One of the best features of the dev server is [Hot Module Replacement](https://webpack.github.io/docs/hot-module-replacement.html) (HMR). This is a feature provided by `webpack-dev-server` that will update specific modules live. In other words, we can potentially update specific parts of our app without having the refresh the entire page.

1. In `webpack.config.js`, `require` `webpack`.

1. HMR is a plugin, so add the following to the `module.exports` object from `webpack.config.js`:

  ```js
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ]
  ```

1. Inside the `devServer` object in `webpack.config.js`, add `hot: true`.

1. Restart the server with `npm start`.  Try making changes to `js/component.js`; you should see the page update automatically. Everytime we make a change to a JavaScript file and save, the browser is automatically updated!

## Add in CSS Watching with Loaders

**Goal**: Automatically update the styles in the browser when CSS files change.

1. Install another package for this: `npm install css-loader style-loader --save-dev`.

1. Add the use of this package in as a module within `webpack.config.js`'s '`module.exports` variable after `output`:

  ```js
  module: {
    loaders: [
      {
        // match all .css files
        test: /\.css$/,
        loaders: ['style', 'css'],
        // Include accepts either a path or an array of paths.
        include: path.join(__dirname, 'css')
      }
    ]
  }
  ```

<!-- 1. If you run `npm start` now, an error about "Promise" will pop up. This is an ES6 bug that can be fixed with [an extra package called es6-promise](https://github.com/stefanpenner/es6-promise#nodejs):

  `npm install es6-promise`

  `var Promise = require('es6-promise').Promise;` -->


1. Go to your `style.css` and change the background to a very visible color. What happens?? Notice how the page does *not* refresh!

## Closing Thoughts

1. What type of tasks can build tools help us to automate?
2. Where do we save all of our Gulp dependencies?
3. What is the difference between `gulp.src()` and `gulp.dest()`?
4. What does the `gulp connect` plugin allow us to do?
5. How do Gulp and Webpack differ?
6. What kinds of things can we configure in `webpack.config.js`?
7. What is a Webpack loader?
8. What are the Webpack `entry` and `output` for?

### Additional Resources

[Webpack as middleware](https://webpack.github.io/docs/webpack-dev-middleware.html)

[Webpack compared](http://survivejs.com/webpack/webpack-compared/)

[Webpack tutorials](http://survivejs.com/webpack_react/developing_with_webpack/)

[Gulp Tutorial](https://scotch.io/tutorials/automate-your-tasks-easily-with-gulp-js)

[Grunt Tutorial](http://www.brianchu.com/blog/2013/07/11/grunt-by-example-a-tutorial-for-javascripts-task-runner/)
