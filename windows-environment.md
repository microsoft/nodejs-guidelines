# Configuring your Windows development environment
## Command line console and other useful tools
One of the pain points we hear from users is that the command line console in Windows could use some work. We hear ya, and we're [working on it](https://wpdev.uservoice.com/forums/266908). In the meantime, we want to enable you to have the best experience possible. So here are some links to recommended tools to complement your existing experience.
* **cmd:** cmd has had some improvements in Windows 10, so be sure to check it out if you abandoned ship in the past :smiley:. When you're working with Node.js, chances are you'll be spending a bit more time in the console, so it's well worth brushing up on your CLI commands.
* **PowerShell:** PowerShell is a powerful object-oriented shell (as opposed to a text-based shell). It's a bit of a learning curve, but well worth it. It also has a bunch of aliases for commands, like `ls`, that'll make bash-happy people feel more at home. Here's a [good walkthrough](https://developer.rackspace.com/blog/powershell-101-from-a-linux-guy/) of some PowerShell commands from a *nix perspective, and there are [many other resources](https://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx) to help you get started.
* **Chocolatey:** [Chocolatey](https://chocolatey.org) is the apt-get of Windows. There are also some other alternatives like Ninite which have their own advantages, but Chocolatey is the most commonly used.
* **Git:** `choco install git`.
* **nvm-windows:** https://github.com/coreybutler/nvm-windows - there are new versions of Node.js coming out all the time, so it can be annoying to migrate between versions. nvm-windows makes it way easier to switch between various versions.
* **npm-windows-upgrade:** npm is shipped with Node.js, and upgrading on Windows often requires manual upgrade steps. npm-windows-upgrade makes this process much easier. Install it by running `npm install npm-windows-upgrade -g`, and run the command by running `npm-windows-upgrade`.
* **terminal emulators:** cmder and ConEmu.
* **Cygwin:** [Cygwin](http://cygwin.com/index.html) can be handy if you're more familiar with bash, or are trying to use a Node app that assumes a *nix environment. Cygwin is a distribution of popular GNU and other open source tools running on Microsoft Windows. The core part is the Cygwin library which provides the POSIX system calls and environment these programs expect.
* **Git for Windows** [Git for windows](https://git-for-windows.github.io/) provides native versions of the BASH shell and some *nix utilites in addition to the command line git and GUI tool. It is probably the best of shells based on MSYS/MinGW but still supplies ports of older versions of the *nix utilities. Works very well in combination with [ConEmu](https://conemu.github.io/).    
* **GitHub Desktop** [GitHub Desktop](https://desktop.github.com/) (previosuly GitHub for Windows) is primarilarly a GUI but it also includes a version of MSYS/MinGW Bash.  
* **Putty:** ssh client.
* **WinSCP:** free [S]FTP client, also supports SCP and webDAV.
* **Fiddler:** a web debugging tool. In general, people use it for the browser-side debugging, but you can also [configure it](http://stackoverflow.com/questions/8697344/can-a-proxy-like-fiddler-be-used-with-node-jss-clientrequest) to view server-side requests from Node.js.

> :triangular_flag_on_post: **TODO** Provide more dev environment options and a PowerShell script to make things easier.

> :chart_with_upwards_trend: **IN PROGRESS** We're currently planning the next Windows release, so it's a great time to let us know your biggest command line pain points!

## Editors and IDEs
* **[Visual Studio Code](https://code.visualstudio.com/)** is a light weight code editor. Yet, it offers powerful capabilies in [editing](https://code.visualstudio.com/Docs/editor/editingevolved),  [debugging](https://code.visualstudio.com/Docs/editor/debugging), and [git integration](https://code.visualstudio.com/Docs/editor/versioncontrol) for [Node.js development](https://code.visualstudio.com/docs/runtimes/nodejs). Code  It is free and available on your favorite platform - Windows, Mac, and Linux. For more information, check out: http://johnpapa.net/visual-studio-code. Several Visual Studio Code extension may be useful for Node.js development:
* [eslint](https://marketplace.visualstudio.com/items/dbaeumer.vscode-eslint) integrates the `eslint` linter.
* [npm script runner](https://marketplace.visualstudio.com/items/eg2.vscode-npm-script) supports to run npm scripts from the command palette.
* [EditorConfig](https://marketplace.visualstudio.com/items/chrisdias.vscodeEditorConfig) consistent editor spaces and indents.

* **[Node.js Tools for Visual Studio](https://aka.ms/explorentvs)** is a free, open-source extension that turns Visual Studio into a powerful Node.js IDE: intelligent code completions, advanced debugging and profiling, cloud deployment, unit-testing, REPL window, and more. For more information, check out these [walkthrough](https://channel9.msdn.com/events/Visual-Studio/Connect-event-2015/801) and  [overview](https://channel9.msdn.com/Blogs/Seth-Juarez/Nodejs-Tools-for-Visual-Studio) videos. Note that while Visual Studio can be used as a stand-alone additional IDE 'layer' to a comprehensive commandline based workflow, several Visual Studio extensions may also prove useful:
  * [EditorConfig](https://visualstudiogallery.msdn.microsoft.com/c8bccfe2-650c-4b42-bc5c-845e21f96328) consistent editor spaces and indents.
  * [NPM scripts task runner](https://visualstudiogallery.msdn.microsoft.com/8f2f2cbc-4da5-43ba-9de2-c9d08ade4941) adds npm scripts to the Visual Studio task runner explorer.
  * [Web Analyzer](https://visualstudiogallery.msdn.microsoft.com/6edc26d4-47d8-4987-82ee-7c820d79be1d) various linting tools incl. ESLint.
  * [Web Essentials](https://visualstudiogallery.msdn.microsoft.com/ee6e6d8c-c837-41fb-886a-6b50ae2d06a2) many useful tools for client and server dev.
  * [GitHub Extensions for Visual Studio](https://visualstudiogallery.msdn.microsoft.com/75be44fb-0794-4391-8865-c3279527e97d) (can installed by selecting during VS installation).

## MAX_PATH explanation and workarounds
For the uninitiated, MAX_PATH is a limitation with many Windows tools and APIs that sets the maximum path character length to 260 characters. There are some workarounds involving UNC paths, but unfortunately not all APIs support it, and that's not the default. This can be problematic when working with Node modules because dependencies are often installed in a nested manner.

### Workarounds

* :heart: Start in a short path (e.g. c:\src)
* `> npm install -g rimraf`
  delete files that exceed max_path
* `> npm dedupe`
  moves duplicate packages to top-level
* `> npm install -g flatten-packages`
  moves all packages to top-level, but can cause versioning issues
* :heart: Upgrade to npm@3 which attempts to the make the `node_modules` folder heirarchy maximally flat. 
  * Ships with Node v5
  * Or… > npm install –g npm-windows-upgrade
* Future:
  * .NET file APIs:
    * The plan: https://www.youtube.com/watch?v=lpa2OFauASM
    * Progress :tada: https://github.com/dotnet/corefx/issues/645

For additional discussion, please see https://github.com/Microsoft/nodejstools/issues/69

## Compiling native Addon modules
There are three primary reasons you might be interested in this section:
* you have an existing C++ library you'd like to take advantage of in your Node.js application
* you are interested in optimizing the performance of some code by writing it in C++
* you're running into dreaded `node-gyp` issues and have no idea what's going on.

### Identifying native modules
How do you know if an npm package you want to install is a native module? Look for `nan`, `node-gyp`, or `node-pre-gyp` dependencies.

### C++ and Node.js? Tell me more...
* Node.js Addon documentation: https://nodejs.org/api/addons.html
* NodeSchool tutorial https://github.com/workshopper/goingnative

### Environment setup and configuration:
#### Prerequisites
**Option 1: Standalone C++ Build Tools (Technical Preview)**

1. Install [VC++ Build Tools Technical Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49983)
> :bulb: [Windows 7 only] requires [.NET Framework 4.5.1](http://www.microsoft.com/en-us/download/details.aspx?id=40773)

2. Install [Python 2.7](https://www.python.org/downloads/), and add it to your `PATH` (by selecting the option in the installer or manually afterwards) 
3. Launch cmd and run:
  * `npm config set python python2.7`
  * `npm config set msvs_version 2015 --global` (this is instead of `npm install [package name] --msvs_version=2015` every time.)
4. *SO MUCH npm install* :tada:

**Option 2: Visual Studio 2015** (takes longer)
* Download Python 2.7 (3.x will not work)
* Download Visual Studio 2015 (free Community Edition and Express for Desktop work)

 > :bulb: During installation, be sure to check the the C++ option.

> :chart_with_upwards_trend: **IN PROGRESS** there are currently two efforts underway to make it easier to install native modules.
  * We recognize that installing full VS can be burdensome, so we're investigating ways to provide a bundle with just the required compiler dependencies on Windows. Watch [this thread](https://github.com/nodejs/node-gyp/issues/629) for updates.
  * There are [long-term](https://github.com/nodejs/build/issues/151) efforts underway to build and cache pre-compiled packages on a server to get rid of compiler dependencies altogether.

#### Verify everything's working
Here are a few packages you can try installing to see if your environment is set up properly.
* bson
* bufferutil
* kerberos
* node-sass
* sqlite3
* phantomjs
* utf-8-validate

#### Resolving common issues

| Errors about...                                              | Issue                                                             | Resolution                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------------------------------|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Python**                                                   | Python 2.7 is not installed or can't be found                     | <ul> <li>Install Python 2.7 and add to PATH</li> <li>Specifiy --python=2.7 during npm install</li> <li>npm config set python 2.7 to set default</li> </ul>                                                                                                                                                                                                                                              |
| **Inability to find msbuild, Visual Studio, or VC compiler** | VC compiler not installed, or environment not properly configured | <ul> <li>Install VC++ compiler</li> <li>Specify --msvs_version=2015 (or other VS version)</li> <li>npm config set msvs_version 2015 -g</li> </ul>                                                                                                                                                                                                                                                       |
| **NaN/Node/v8/iojs-related syntax errors**                   | Package incompatible with current version of Node.js              | <ul> <li>Upgrade to latest version of package + node.js, and see if issue still exists</li> <li>Search issues and/or file an issue on package repo</li> </ul>                                                                                                                                                                                                                                           |
| **Other syntax errors**                                      | Incompatible with compiler version                                | <ul> <li>Upgrade to latest version of package + node.js, and see if issue still exists</li> <li>Search issues and/or file an issue on package repo</li> </ul>                                                                                                                                                                                                                                           |
| **Missing command or *.h file**                              | Configuration is probably fine, but missing other prerequisites   | <ul> <li>Upgrade to latest version of package</li> <li>Check docs, try to install missing prerequisites, ensure they're accessible in PATH</li> <li>Search for header file or other pre-requisite that's missing, that may provide a clue where it's supposed to come from (e.g. Windows SDK not installed, OpenSSL, etc.)</li> <li>Search issues and/or file an issue on package repository</li> </ul> |

#### Deploying native modules
Sometimes, when deploying a native module to production, oftentimes it is not possible to set up the production machine with all the required prerequisites to build the native Addon. Therefore, building locally or on a CI server and deploying `node_modules` may be the best option assuming there aren't any platform differences between the development and deployment machines.
