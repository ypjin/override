# Override

Override is a general purpose middleware framework for Node.js that lets you 
override and extend built in functionality.

Override modules are executed in sequence before your main module is loaded, making 
it possible to run additional code on startup & modify built in prototypes and 
functions.

For example, override modules make it possible to replace the built in `console.log` 
with a version that sends the logs to a third party service, chroot the current process,
enable profiling etc. etc.

## Installation

Install `override` as a global package (use `sudo` if you're on Ubuntu or Mac):

```bash
npm -g install override
```

## Usage

To run your app via `override` replace the call to `node` with `node-override` passing
in your Override environment as the first parameter. So instead of `node index.js`, use 
`node-override -e mylog,simple index.js`. 

## Environments

Override environments are simply comma separated lists of Override package or module names. You may for example have a different environment for development, staging and production.

You can avoid specifying the environment every time you run your app by setting the `OVERRIDE_ENV` environment variable.

For example on *nix you can do this with:

```bash
export OVERRIDE_ENV=mylog,simple
``` 

## Override Modules

Override modules have the following signature:

```js
module.exports = function(next) {
  console.log('Hello Override!');
  next();
}
```

Here, the code outside of the exported function runs in a clean environment, before any overrides have had effect.

The exported function accepts a single parameter, which is the next function to call in the override middleware chain. 
The middleware chain terminates with the loading of the app's main module. As such any calls after `next()` will take 
place after the main module has been loaded.

Use [environment variables](http://nodejs.org/api/process.html#process_process_env) to pass configuration parameters to your module.

You can find more Override module examples in the 'examples` sub-directory.

Override modules can be distributed as packages via NPM. The convention is to prefix the name with `or-`. This 
makes it easy to [search for them on GitHub](https://github.com/search?q=or-*&repo=&langOverride=&start_value=1&type=Repositories&language=JavaScript).

## License 

(The MIT License)

Copyright (c) 2012+ Oleg Podsechin

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

