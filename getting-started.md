## Getting Started with Node and NPM
Let's start with the basics.

1. Install Node.js: https://nodejs.org.
> :bulb: This code will need at least version 5.0.0, but we encourage you to run at least version 10.0.0. If you already had node installed, make sure the version is appropriate by running `node -v`

> :bulb: When you install Node.js, you'll want to ensure your `PATH` variable is set to your install path so you can call Node from anywhere.

2. Create a new directory named `hello-world`, add a new `app.js` file:
  ```js
  /* app.js */
  console.log('Hello World!');
  ```

3. In the command prompt, run `node app.js`.
> :bulb: Your environment variables are set at the time when the command prompt is opened, so ensure to open a new command prompt since step 1 if you get any errors about Node not being found.

4. Moving beyond from simple console applications...
  ```js
  /* app.js */

  // Load the built-in 'http' module.
  const http = require('http');

  // Create an http.Server object, and provide a callback that fires after 'request' events.
  const server = http.createServer((request, response) => {
    // Respond to the http request with "Hello World" and a basic header.
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.end('Hello World!\n');
  });

  // Try retrieving a port from an environment variable, otherwise fallback to 8080.
  const port = process.env.PORT || 8080;

  // Start listening on the specified port and print out a url to visit.
  server.listen(port);
  console.log(`Listening on http://localhost:${port}`);
  ```

5. In the command prompt, run `node app.js`, and visit the url that's printed out to the console.

6. To stop the application, run `Ctrl+C`.

## Working with npm packages
As shown above, it's pretty impressive what you can do with so few lines of code in Node.js. Part of the philosophy of Node.js is that the core should remain as small as possible. It provides just enough built-in modules, such as filesystem and networking modules, to empower you to build scalable applications. However, you don't want to keep re-inventing the wheel every time for common tasks.

Introducing, npm!

npm is the package manager for JavaScript. npm ships with Node.js, so there's no need to install it separately.

### Using an existing npm package
To get a sense for how to use npm packages in your app, let's try getting started with `express`, the most popular web framework for Node.js.

1. Create a new directory entitled `my-express-app`, then install `express` from within that directory. When `express` is installed, the package and its dependencies appear under a `node_modules` folder.
  ```
  C:\src> mkdir my-express-app
  C:\src> cd my-express-app
  C:\src\my-express-app> npm install express
  ```

  > :bulb: We recommend starting with a short path like C:\src to work around any potential MAX_PATH issues.

2. Now, create a new file, `app.js`. This code will load the express module we just installed, and use it to start a lightweight web server.
  ```js
  /* app.js */

  const express = require('express');
  const app = express();

  app.get('/', (req, res) => {
    res.send('Hello World!');
  });

  const port = process.env.PORT || 3000;
  app.listen(port, () => {
    console.log(`Listening on http://localhost:${port}`);
  });
  ```

3. Start the app by running `node app.js` in the command line. Tada!

There are many more packages available at your disposal (200K and counting!). Head on over to https://www.npmjs.com to start exploring the ecosystem.

> :bulb: Most of the packages available via npm tend to be pure JavaScript, but not all of them. For instance, there's a small percentage of native module addons available via npm that provide Node.js bindings, but ultimately call into native  C++ code. This includes packages with `node-gyp`, `node-pre-gyp`, and `nan` dependencies. In order to install and run these packages, some additional machine configuration is required (described below).

### Managing npm dependencies
Once you start installing npm packages, you'll need a way to keep track of all of your dependencies. In Node.js, you do this through a `package.json` file.

1. To create a `package.json` file, run the `npm init` in your app directory.
  ```
  C:\src\my-express-app> npm init
  ```

2. Npm will prompt you to fill in the details about your package.
3. In the `package.json` file, there is a "dependencies" section, and within it, an entry for `"express"`. A value of `"*"` would mean that the latest version should be used. To add this entry automatically when you install a package, you can add a `--save` flag: `npm install express --save`.To save this as a dev dependency, use `npm install express --save-dev`.
 > :bulb: If you only require a dependency as part of a development environment, then you could/should install the package in the "[devDependencies](http://stackoverflow.com/questions/19223051/grunt-js-what-does-save-dev-mean-in-npm-install-grunt-save-dev)".  This is accomplished by using the `--save-dev` parameter. For example: `npm install --save-dev mocha`.

4. Now that your packages are listed in `package.json`, npm will always know which dependencies are required for your app. If you ever need to restore your packages, you can run `npm install` from your package directory.

> :bulb: When you distribute your application, we recommend adding the `node_modules` folder to `.gitignore` so that you don't clutter your repo with needless files. This also makes it easier to work with multiple platforms. If you want to keep things as similar as possible between machines, npm offers many options that enable you to fix the version numbers in `package.json`, and even more fine-grained control with `npm-shrinkwrap.json`.

### Publishing npm packages to the registry
Once you've created a package, publishing it to the world is only one command away!

`C:\src\my-express-app> npm publish`

> :bulb: Use npm's private modules.

> :triangular_flag_on_post: **TODO** Add description about how to authorize the machine using `npm adduser`.

### Local vs. global packages
There are two types of npm packages - locally installed packages and globally installed packages. It's not an exact science, but in general...
* Locally installed packages are packages that are specific to your application
* Globally installed packages tend to be CLI tools and the like

We went through locally installed packages above, and installing packages globally is very similar. The only difference is the `-g` command.

1. `npm install http-server -g` will install the module globally.

  > :bulb: The module will be installed to the path indicated by `npm bin -g`.

2. Run `http-server .` to start a basic fileserver from any directory. On running this command , the server starts and runs on the localhost.

> :bulb: In fact the only difference when using -g is that executables are placed in a folder that is on the path. If you install without the -g option you can still access those executables in `.\node_modules\.bin`. This folder is automatically added to the path when any scripts defined in `package.json` are run. Doing this will help avoid version clashes when a project uses skrinkwrap or otherwise specifies the version of a module different to other projects. It also avoids the need for manual install instructions for some dependencies so a single "npm install" will do.

### And much more!
* [npm docs and tutorials](https://docs.npmjs.com/)
* [Laurie Voss - npm past, present, and future](https://www.youtube.com/watch?v=-fqu-5IuOkc)

## Using nodemon

[nodemon](http://nodemon.io/) is a utility that will monitor for any changes in your source and automatically restart your server. Use npm to install it:

```
npm install -g nodemon
```` 

After installation, you can launch your application using nodemon. For example: 

```
nodemon app.js
``` 

After this, you don't have to restart the Node server after making changes since nodemon will automatically restart it for you. If you're developing a web application, simply refresh your browser to examine your update. Pretty handy for development!
