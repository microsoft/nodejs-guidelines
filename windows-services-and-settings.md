## Working with Windows Services and Settings

### Reading and Writing to the Windows Registry in-process from Node.js
As cross-platform application developers, we often need the ability to update the Windows Registry when installing our applications to Windows. [NPM module for Windows Registry](https://www.npmjs.com/package/windows-registry) is an npm package that can be included in your node applications to allow reading and writing keys to Windows registry, creating file associations, and elevating processes to run as an administrator in-process from Node.js.

This library leveraged [node-ffi](https://www.npmjs.com/package/ffi), [ref](https://www.npmjs.com/package/ref),[ref-struct](https://www.npmjs.com/package/ref-struct), [Advapi32.dll](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724875(v=vs.85).aspx), and [Shell32.dll](https://msdn.microsoft.com/en-us/library/windows/desktop/bb762154(v=vs.85).aspx) to enable Node.js applications to communicate with Windows interfaces. 

#### Prerequisites
Follow the [Environment setup and configuration](https://github.com/Microsoft/nodejs-guidelines/blob/master/windows-environment.md#environment-setup-and-configuration) section to compile native addon modules. 

#### Install

This library interacts with native Windows APIs. To add this module to your Node application, install the package:

```
npm install windows-registry

```

#### Creating File Associations

To create a file association, you can call the `fileAssociation.associateExeForFile` API, which will make windows assign a default program for an arbitrary file extension:

```js
var utils = require('windows-registry').utils;
utils.associateExeForFile('myTestHandler', 'A test handler for unit tests', 'C:\\path\\to\\icon', 'C:\\Program Files\\nodejs\\node.exe %1', '.zzz');

```
After running the code above, you will see files with the extension of `.zzz` will be automatically associated with the Node program and their file icon will be changed to the Node file icon.

#### Reading and Writing to the Windows Registry

This library implements only a few of the basic registry commands, which allow you to do basic CRUD 
operations for keys in the registry.

#### Opening a Registry Key

Registry keys can be opened by either opening a predefined registry key defined in the [windef](lib/windef.js) module:

```js
var Key = require('windows-registry').Key;
var key = new Key(windef.HKEY.HKEY_CLASSES_ROOT, '.txt', windef.KEY_ACCESS.KEY_ALL_ACCESS);

```

Or you can open a sub key from an already opened key:

```js
var Key = require('windows-registry').Key;
var key = new Key(windef.HKEY.HKEY_CLASSES_ROOT, '', windef.KEY_ACCESS.KEY_ALL_ACCESS);
var key2 = key.openSubKey('.txt', windef.KEY_ACCESS.KEY_ALL_ACCESS);

```

And don't forget to close your key when you're done. Otherwise, you will leak native resources:

```js
key.close();

```

#### Creating a Key

Creating a key just requires that you have a [Key](lib/key.js) object by either using the [predefined keys](https://github.com/CatalystCode/windows-registry-node/blob/master/lib/windef.js#L27) within the `windef.HKEY` or opening a subkey from an existing key.

```js
var Key = require('windows-registry').Key;
// predefined key
var key = new Key(windef.HKEY.HKEY_CLASSES_ROOT, '', windef.KEY_ACCESS.KEY_ALL_ACCESS);
var createdKey = key.createSubKey('\test_key_name', windef.KEY_ACCESS.KEY_ALL_ACCESS);

```

#### Deleting a Key
To delete a key just call the `Key.deleteKey()` function.

```js
createdKey.deleteKey();

```

#### Writing a Value to a Key

To write a value, you will again need a [Key](lib/key.js) object and just need to call the `Key.setValue` function:

```js
var Key = require('windows-registry').Key,
	windef = require('windows-registry').windef;

var key = new Key(windef.HKEY.HKEY_CLASSES_ROOT, '.txt', windef.KEY_ACCESS.KEY_ALL_ACCESS);
key.setValue('test_value_name', windef.REG_VALUE_TYPE.REG_SZ, 'test_value');

``` 

#### Get a Value From a Key

To get a value from a key, just call `Key.getValue`:

```js
var value = key.getValue('test_value_name');
```

The return value depends on the type of the key (REG_SZ for example will give you a string).

#### Launching a Process as an Admin

To launch a process as an Administrator, you can call the `utils.elevate` API, which will launch a process as an Administrator causing the UAC (User Account Control) elevation prompt to appear if required. This is similar to the Windows Explorer command "Run as administrator".  Pass in `FILEPATH` to the process you want to elevate. Pass in any`PARAMETERS` to run with the process. Since this is an asynchronous call, pass in a callback to handle user's selection.

```js
var utils = require('windows-registry').utils;
utils.elevate('C:\\Program Files\\nodejs\\node.exe', 'index.js', function (err, result){console.log(result);});

```
The process you want to launch with admin access will only be launched after the callback is called and only if the user clicks Yes in the UAC prompt. Otherwise, the process will not be launched. If the user is already running as an admin, the UAC prompt will not be triggered and the process you provided will be launched as an administrator automatically.

#### More Examples and Docs?
Check out implementation details of this module: https://github.com/CatalystCode/windows-registry-node.