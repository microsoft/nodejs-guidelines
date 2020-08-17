# Configuring your Windows development environment

## Command line console and other useful tools
One of the pain points we hear from users is that the command line console in Windows could use some work. We hear ya, and we're [working on it](https://wpdev.uservoice.com/forums/266908). In the meantime, we want to enable you to have the best experience possible. So here are some links to recommended tools to complement your existing experience.
* **cmd:** cmd has had some improvements in Windows 10, so be sure to check it out if you abandoned ship in the past :smiley:. When you're working with Node.js, chances are you'll be spending a bit more time in the console, so it's well worth brushing up on your CLI commands.
* **PowerShell:** PowerShell is a powerful object-oriented shell (as opposed to a text-based shell). It's a bit of a learning curve, but well worth it. It also has a bunch of aliases for commands, like `ls`, that'll make bash-happy people feel more at home. Here's a [good walkthrough](https://developer.rackspace.com/blog/powershell-101-from-a-linux-guy/) of some PowerShell commands from a *nix perspective, and there are [many other resources](https://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx) to help you get started.
* **Chocolatey:** [Chocolatey](https://chocolatey.org) is the apt-get of Windows. There are also some other alternatives, like [Ninite](https://ninite.com/), which have their own advantages, but Chocolatey is the most commonly used.
* **Git:** `choco install git` or download Git from [the official downloads page](https://git-scm.com/downloads).
* **nvm-windows:** https://github.com/coreybutler/nvm-windows - there are new versions of Node.js coming out all the time, and it can be annoying to migrate between versions. nvm-windows makes it way easier to switch between various versions.
* **npm-windows-upgrade:** npm is shipped with Node.js, and upgrading on Windows often requires manual upgrade steps. npm-windows-upgrade makes this process much easier. Install it by running `npm install npm-windows-upgrade -g`, and run the command by running `npm-windows-upgrade`.
* **terminal emulators:** Terminal emulators can enhance your terminal experience with themes, tabs and advanced configuratability. Popular emulators include [cmder](http://cmder.net/), [ConEmu](https://conemu.github.io/) and [Hyper](https://hyper.is/).
* **Cygwin:** [Cygwin](http://cygwin.com/index.html) can be handy if you're more familiar with bash, or are trying to use a Node app that assumes a *nix environment. Cygwin is a distribution of popular GNU and other open source tools running on Microsoft Windows. The core part is the Cygwin library which provides the POSIX system calls and environment these programs expect.
* **Git for Windows** [Git for windows](https://git-for-windows.github.io/) provides native versions of the BASH shell and some *nix utilites in addition to the command line git and GUI tool. It is probably the best of shells based on MSYS/MinGW but still supplies ports of older versions of the *nix utilities. Works very well in combination with [ConEmu](https://conemu.github.io/).    
* **GitHub Desktop** [GitHub Desktop](https://desktop.github.com/) (previously GitHub for Windows) is primarilarly a GUI but it also includes a version of MSYS/MinGW Bash.  
* **Putty:** an SSH and telnet client: https://www.putty.org/.
* **WinSCP:** an (S)FTP client that also supports SCP and webDAV: https://winscp.net/.
* **Fiddler:** a web debugging tool: https://www.telerik.com/fiddler. In general, people use it for the browser-side debugging, but you can also [configure it](http://stackoverflow.com/questions/8697344/can-a-proxy-like-fiddler-be-used-with-node-jss-clientrequest) to view server-side requests from Node.js.

> :triangular_flag_on_post: **TODO** Provide more dev environment options and a PowerShell script to make things easier.

> :chart_with_upwards_trend: **IN PROGRESS** We're currently planning the next Windows release, so it's a great time to let us know your biggest command line pain points!

## Editors and IDEs
* **[Visual Studio Code](https://code.visualstudio.com/)** is a lightweight, cross-platform IDE that offers powerful [editing](https://code.visualstudio.com/Docs/editor/editingevolved), [debugging](https://code.visualstudio.com/Docs/editor/debugging), and [version control integration](https://code.visualstudio.com/Docs/editor/versioncontrol) for [Node.js development](https://code.visualstudio.com/docs/runtimes/nodejs). Several Visual Studio Code extension may be useful for Node.js development:
  * [eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) integrates the `eslint` linter.
  * [npm script runner](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script) adds support for running npm scripts from the command palette.
  * [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) helps enforce consistent editor spaces and indents.

* **[Node.js Tools for Visual Studio](https://aka.ms/explorentvs)** is a free, open-source extension that turns Visual Studio into a powerful Node.js IDE: intelligent code completions, advanced debugging and profiling, cloud deployment, unit-testing, REPL window, and more. For more information, check out these [walkthrough](https://channel9.msdn.com/events/Visual-Studio/Connect-event-2015/801) and  [overview](https://channel9.msdn.com/Blogs/Seth-Juarez/Nodejs-Tools-for-Visual-Studio) videos. Note that while Visual Studio can be used as a stand-alone additional IDE 'layer' to a comprehensive commandline based workflow, several Visual Studio extensions may also prove useful:
  * [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfigTeam.EditorConfig) helps enforce consistent editor spaces and indents.
  * [NPM scripts task runner](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.NPMTaskRunner) adds support for running npm scripts from the Visual Studio task runner explorer.
  * [Web Analyzer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebAnalyzer) provides various linting tools, including the `eslint` linter.
  * [Web Essentials](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebEssentials20153) adds many useful tools for client and server dev.
  * [GitHub Extensions for Visual Studio](https://marketplace.visualstudio.com/items?itemName=GitHub.GitHubExtensionforVisualStudio) makes it easy to connect to and work with GitHub repositories and can installed during Visual Studio installation.

* **[WebStorm](https://www.jetbrains.com/webstorm/)** is a lightweight yet powerful IDE, perfectly equipped for complex client-side development and server-side development with Node.js. It boasts [a lot of features](https://www.jetbrains.com/webstorm/features/), including support for both JavaScript and TypeScript, framework support (Angular, React, Vue.js, Meteor, etc.), code quality tools (TSLint, ESLint, etc.), build tools (Gulp, Grunt or npm), debugging, testing and more.


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
    * From Windows 10 Preview build 14352 (and the upcoming Anniversary edition due late July) there is an [opt-in policy](http://betanews.com/2016/05/29/long-paths-windows-10/) to remove the MAX_PATH Limit !!!!!  
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

* Option 1: Install all the required tools and configurations using Microsoft's [windows-build-tools](https://github.com/felixrieseberg/windows-build-tools) by running `npm install -g windows-build-tools` from an elevated PowerShell (run as Administrator).

* Option 2: Install dependencies and configuration manually
    1. Install Visual C++ Build Environment: [Visual Studio Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools) (using "Visual C++ build tools" workload) or [Visual Studio 2017 Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community) (using the "Desktop development with C++" workload)
    2. Install [Python 2.7](https://www.python.org/downloads/) (`v3.x.x` is not supported), and run `npm config set python python2.7`
    3. Launch cmd, `npm config set msvs_version 2017`

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

| Errors about...                                              | Issue                                                                | Resolution                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------ | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Python**                                                   | Python 2.7 is not installed or can't be found                        | <ul> <li>Install Python 2.7 and add to PATH</li> <li>Specifiy --python=2.7 during npm install</li> <li>npm config set python 2.7 to set default</li> </ul>                                                                                                                                                                                                                                         |
| **Inability to find msbuild, Visual Studio, or VC compiler** | VC compiler not installed, or environment not properly configured    | <ul><li>Install VC++ compiler</li><li>Specify --msvs_version=2015 (or other VS version)</li><li>npm config set msvs_version 2015 -g</li></ul>                                                                                                                                                                                                                                                      |
| **NaN/Node/v8/iojs-related syntax errors**                   | Package incompatible with current version of Node.js                 | <ul><li>Upgrade to latest version of package + node.js, and see if issue still exists</li><li>Search issues and/or file an issue on package repo</li></ul>                                                                                                                                                                                                                                         |
| **Other syntax errors**                                      | Incompatible with compiler version                                   | <ul><li>Upgrade to latest version of package + node.js, and see if issue still exists</li><li>Search issues and/or file an issue on package repo</ul>                                                                                                                                                                                                                                              |
| **Missing command or \*.h file**                             | Configuration is probably fine, but missing other prerequisites      | <ul><li>Upgrade to latest version of package</li><li>Check docs, try to install missing prerequisites, ensure they're accessible in PATH</li><li>Search for header file or other pre-requisite that's missing, that may provide a clue where it's supposed to come from (e.g. Windows SDK not installed, OpenSSL, etc.)</li><li>Search issues and/or file an issue on package repository</li></ul> |
| **MSB4019 error**                                            | Older versions of Visual Studio or C++ Build tools already installed | <ul><li>Add or modify the environment variable `VCTargetsPath` top point at the C++ build tools path. This should be something like `C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\v140` (where 140 corresponds to Visual Studio 2015)</li><li>Search issues and/or file an issue on package repo</li></ul>                                                                                    |
| **__pfnDliNotifyHook2 redefinition error**                   | latest version of npm seems to fix this                              | Run `npm -g install npm@next`                                                                                                                                                                                                                                                                                                                                                                      |


#### Deploying native modules
Sometimes, when deploying a native module to production, oftentimes it is not possible to set up the production machine with all the required prerequisites to build the native Addon. Therefore, building locally or on a CI server and deploying `node_modules` may be the best option assuming there aren't any platform differences between the development and deployment machines.
