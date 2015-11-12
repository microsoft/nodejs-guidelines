## Writing cross-platform modules and apps
* http://shapeshed.com/writing-cross-platform-node/
* https://gist.github.com/domenic/2790533

## Accessing platform APIs
Sometimes you need to access plaform functionality for which no suitable module is available. For example your product may need to access the registry running on a Windows Server or Desktop. In this case there are 2 ways to proceed. 

1. Create a native module add-on by wrapping code in C binding boilerplate code [using the V8 sdk and dev tools](https://nodejs.org/api/addons.html).
2. Use [ref](https://github.com/TooTallNate/ref) and [node-ffi](https://github.com/node-ffi/node-ffi) modules to access C buffers and call shared library (DLL) functions from javascript.

There are plenty of examples of [creating native modules](http://www.martinchristen.ch/node/tutorial11) incuding our notes on [Compiling native addon modules](windows-environment.md#compiling-native-addon-modules)but not so much on [of node-ffi](http://opendirective.net/blog/2015/10/working-with-windows-native-code-from-node-js)

> :bulb: Note it is good practice to ensure published modules work on all platforms as discussed above, even though this can be conciderable work. While there are no doubt exceptions, such accessing the Windows registry, modules that only work on Windows or Linux are likely to unpopular.

