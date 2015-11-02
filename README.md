# Microsoft + Node.js Guidelines
Microsoft :heart: Node.js, and we want to make sure your experience is as seamless as possible.

In particular, our goals here are to:
* make it easier for people using Microsoft platforms and technologies to get started on the right foot with Node.js
* consolidate our Node.js offerings in a centralized place so it's easier to build compelling end-to-end stories.
* provide a forum to connect with various teams at Microsoft working to improve the Node.js experience
* communicate status on key issues we're helping to address

Note that this is not intended to be a comprehensive set of recommendations, nor is it meant to be a tutorial. Rather it's meant to be a helpful set of content that makes it easier to avoid any potential gotchas, and the beginning of what we expect to be an ongoing conversation on how we can improve the Node.js experience on Microsoft platforms.

## "Hello, World"
Let's start with the basics. 

1. Install Node.js: https://nodejs.org
> :bulb: when you install Node.js, you'll want to ensure your `PATH` variable is set to your install path so you can call Node from anywhere.

2. create a new directory named `hello-world`, add a new `app.js` file:
  ```js
  /* app.js */
  console.log('Hello, world!')
  ```
 
3. In the commmand prompt, run `node app.js`
> :bulb: your environment variables are set a the time that the command prompt was opened, so ensure you've opened a new command prompt since step 1 if you get any errors about Node not being found.

4. Moving beyond from simple console applications...
  ```js
  /* app.js */
  
  // Load the built-in 'http' module
  var http = require('http');

  // Create an http.Server object, and provide a callback that fires after 'request' events
  var server = http.createServer(function (request, response) {
     // Respond to the http request with "Hello World" and a basic header
     response.writeHead(200, {'Content-Type': 'text/plain'});
     response.end('Hello World\n');
  });

  // Try retrieving a port from an environment variable, otherwise fallback to 8080.
  var port = process.env.PORT || 8080;
  
  // Start listening on the specified port and print out a url to visit.
  server.listen(port);
  console.log('Listening on http://localhost:' + port);
  ```

5. In the commmand prompt, run `node app.js`, and visit the url that's printed out to the console.

## Working with npm packages
As shown above, it's pretty impressive what you can do with so few lines of code in Node.js. But part of Node.js's philosophy is that the core should remain as small as possible... providing just enough built-in filesystem / networking modules, and the like to empower people to build powerful and scalable applications. But you also don't want to keep re-inventing the wheel every time you want to do something simple. 

Introducing, npm! npm doesn't stand for "Node package manager", but it *is* Node.js's package manager. Npm ships with Node.js, so there's no need to install anything new. 

### Using an existing npm package
To get a sense for how to use npm packages in your app, let's try getting started with Express, which is the most popular Node.js webframework.

1. Create a new directory entitled `my-express-app`, then install `express` from within that directory. When express is installed, you'll new entries for `express` and it's dependencies appear under a `node_modules` folder.
  ```
  C:\src> mkdir my-express-app
  C:\src> cd my-express-app
  C:\src\my-express-app> npm install express
  ```
  
  > :bulb: We recommend starting with a short path like C:\src to work around any potential MAX_PATH issues

2. Now, create a new file, `app.js` as we did above past. This code will load the express module we just installed, and use it to start a lightweight server.
  ```js
  /* app.js */
  
  var express = require('express');
  var app = express();
 
  app.get('/', function (req, res) {
    res.send('Hello World');
  })
 
  var port = process.env.PORT || 3000;
 
  app.listen(port);
  console.log('Listening on http://localhost:' + port);
  ```

3. Start the app by running `node app.js` in the command line.

Tada! There are many many more packages available at your disposal (200K and counting!). Head on over to https://www.npmjs.com/ to start exploring the ecosystem.

> :bulb: Most of the packages available via npm tend to be pure javascript, but not all of them. For instance, there's a small percentage of native module addons available via npm that provide Node.js bindings, but ultimately call into native  C++ code. This includes packages with `node-gyp`, `node-pre-gyp`, and `nan` dependencies. In order to install and run these packages, some additional machine configuration is required (described below.)

### Managing your npm dependencies
Once you start installing npm packages, you'll need a way to keep track of all of your dependencies. In Node.js, you do this through a package.json file. 

1. To create a package.json file, run the `npm init` in your app directory. 
  ```
  C:\src\my-express-app> npm init
  ```
  
2. Npm will prompt you to fill in any details about your package.
3. In the package.json file, add a "dependencies" section, and within it, specify 

### Publishing npm packages to the registry
Once you've created a package, publishing it to the world is only one command away!
`C:\src\my-express0app> npm publish`

### Local vs. Global packages
There are two types of npm packages - locally installed packages and globally installed packages. It's not an exact science, but in general...
* Locally installed packages are packages that are specific to your application
* Globally installed packages tend to be cli tools and the like

## Customizing your Windows development environment
### Command line console
One of the painpoints we hear from users is that the command line console in Windows could use some work. We hear ya, and we're [working on it.](https://wpdev.uservoice.com/forums/266908) In the meantime, we want to ensure you have the best experience possible. So here's some links to some recommended tools to complement your existing experience.

* **Chocolatey:** Chocolatey is the apt-get of Windows. There are also some other alternatives like Ninite which have their own advantages, but Chocolatey is the most commonly used. 

* Git: `choco install git`
* terminal emulators: cmder and conemu
* Powershell
* Cygwin
* WinSCP
* Putty: ssh client
* nvm-windows: https://github.com/coreybutler/nvm-windows - there are new versions of Node.js coming out all the time, so it can be annoying to migrate between versions. nmv-windows makes this way easier to switch between various versions, so we 
* Fiddler: a web debugging proxy for Node.js
* Upgrading npm to the latest version: https://www.npmjs.com/package/npm-windows-upgrade

> :triangular_flag_on_post: **TODO** provide more dev environment options and a powershell script to make things easier.

> :chart_with_upwards_trend: **IN PROGRESS** we're currently planning the next Windows release, so it's a great time to let us know you biggest command line painpoints! 

### Editors and IDEs
* Node.js Tools for Visual Studio
  * End-to-End tooling
    * Node.js Tools for Visual Studio
      * Download the free tools
      * Learn about the end-to-end experience of building a Node.js application in Visual Studio: https://channel9.msdn.com/Blogs/Seth-Juarez/Nodejs-Tools-for-Visual-Studi
      * GitHub repo: https://github.com/Microsoft/nodejstools
    * Alternatives: WebStorm
  * Editors
    * VSCode - light weight and cross-platform

## Compiling native addon modules
There are three primary reasons you might be interested in this section: 
* you have an existing C++ libary you'd like to take advantage of in your Node.js application
* you are interested in optimizing the performance of some code by writing it in C++
* You're running into dreaded node-gyp issues and have no idea what's going on

### Just tell me how to set up my environment!
* Download Python 2.7 (3.x will not work)
* Download Visual Studio 2015 Community
  * during install, be sure to check the the C++ option

> :chart_with_upwards_trend: **IN PROGRESS** there are currently two efforts underway to make it easier to install native modules.
  * We recognize that installing full VS can be burdensome, so we're investigating ways to provide a bundle with just the required compiler dependencies on Windows. Watch [this thread](https://github.com/nodejs/node-gyp/issues/629) for updates.
  * There are [long-term](https://github.com/nodejs/build/issues/151) efforts underway to build and cache pre-compiled packages on a server to get rid of compiler dependencies altogether.

### C++ and Node.js? Tell me more...
* Node.js addon documentation: https://nodejs.org/api/addons.html
* NodeSchool tutorial https://github.com/workshopper/goingnative

## So... how about them MAX_PATH issues?
For the uninitiated, MAX_PATH is a limitation with many windows tools and APIs that sets the maximum path character length to 260 characters. There are some workarounds involving UNC paths, but unfortunately not all APIs support it, and that's not the default. 
> In the Windows API (with some exceptions discussed in the following paragraphs), the maximum length for a path is MAX_PATH, which is defined as 260 characters.
> http://msdn.microsoft.com/en-us/library/windows/desktop/aa365247(v=vs.85).aspx
## Common issues
* MAX_PATH
  * description 
  * deleting/moving files
  * workarounds
  * progress
* node-gyp
  * description
  * setup
  * progress
  * 
  
## Dealing with platform-specific issues and writing portable code
* check for common node.js errors
* https://gist.github.com/domenic/2790533

## IoT development
* Node-Chakra

## Deployment
* Continuous integration with VSO
* Docker and containers
* Cross-platform remote debugging
* iisnode

## Open-source Node.js projects
https://github.com/Microsoft?utf8=%E2%9C%93&query=nodeb


## Application specific tips and tricks
* setting up MongoDB
* setting up SQL
* .NET in-process using Edge.js

### TypeScript and Node.js tips

## Teams at Microsoft supporting Node.js
**This list is incomplete**
* Node.js Tools for Visual Studio: @mousetraps, arunesh
* VSCode: chrisdias
* Azure
* App Insights
* Node core contributors: 

## Teams at Microsoft using Node.js
**TODO**

## Contribution guidelines
