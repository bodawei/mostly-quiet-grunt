# mostly-quiet-grunt

> Limit grunt output to nothing, dots, or very deliberate output if everything goes well. On error print dump everything.

[![NPM info][nodei.co]](https://npmjs.org/package/mostly-quiet-grunt)

[![dependencies][dependencies-image]][dependencies-url]

## The Problem
The default output from Grunt is more verbose than I would like. During a good build, I would prefer to silence all output except for a test report summary at the end.

Like this module's ancestor, [quiet-grunt](https://github.com/bahmutov/quiet-grunt), this will suppress most of the grunt output on a good build. It offers a caller two features that quiet-grunt does not:

* an option to not even show a dot on every message
* a special exposed routine which allows one to bypass the output suppression.

If there is an error, the entire output will be dumped.

## Install

```shell
npm install  --save-dev mostly-quiet-grunt
```

## Use

Once the module has been installed, require it at the beginning of the gruntfile.

```js
const controller = require('mostly-quiet-grunt');

module.exports = function (grunt) {
   ...
   controller.showDots(true);
   controller.passthroughWrite('Show this during the run of grunt.');
   ...
```

If an option `--no-quiet`, `--verbose`, `--noq`, `-v` or the command `watch` is provided, then this will not be turned on.

## What it does
When this module is invoked, if none of the options mentioned above are used, then it will replace the `process.stdout.write(message)` routine with a function that stores the message. When the process then starts to `exit()`, if the exit code is not 0, then write the accumulated messages.

If the `controller.passthroughWrite(message)` function is called, this will bypass the storing process. If `controller.showDots(true|false)` is called, write (or, if false, don't write) a period character each time `process.stdout.write(message)` is called.

## Small print

Author: 柏大衛 &copy; 2017

This is a fork of [bahmutov/quiet-grunt](https://github.com/bahmutov/quiet-grunt). You should use that module unless you particularly want the "nothing" or the "very deliberate outout" this offers.

License: MIT - do anything with the code, but don't blame me if it does not work.

Support: if you find any problems with this module, open an issue on Github.

[nodei.co]: https://nodei.co/npm/mostly-quiet-grunt.png?downloads=true
[dependencies-image]: https://david-dm.org/bodawei/mostly-quiet-grunt.png
[dependencies-url]: https://david-dm.org/bodawei/mostly-quiet-grunt
