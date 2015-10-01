# node-windows-tips
## Setting up a development environment
### Getting to "Hello, World"
* Install Node.js: https://nodejs.org/en/

* Upgrading npm to the latest version: https://www.npmjs.com/package/npm-windows-upgrade

### Customizing your environment
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

### Editors and IDEs
  * End-to-End tooling
    * Node.js Tools for Visual Studio
    * Webstorm
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

### C++ and Node.js? Tell me more...
* Node.js addon documentation: https://nodejs.org/api/addons.html
* NodeSchool tutorial https://github.com/workshopper/goingnative


## Databases
* setting up MongoDB


## Working with .NET
* using Edge.js

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
  
## Writing portable code
* check for common node.js errors
* https://gist.github.com/domenic/2790533

## IoT development
* Node-Chakra

## Deployment
* Continuous integration with VSO
* Docker and containers
* Cross-platform remote debugging
* iisnode

## Node efforts at Microsoft

## Teams at MSFT using Node.js

## Contribution guidelines

## Why does this exist?
This exists because a bunch of people at Microsoft are really excited about Node.js and want to make sure your experience is as awesome as it can possibly be. In particular, our goals here are to:
* make it easier for people building on Microsoft platforms to get started on the right foot
* promote our Node.js offerings in a centralized place so it's easier to iron out compelling end-to-end stories.
* provide a forum to connect with various teams at Microsoft working to improve the Node.js experience
* communicate status on key issues we're helping to address
