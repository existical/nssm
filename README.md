# nssm

Wrapper for `nssm.exe` to manage Windows services with `Promises` support

This is fork of [nssm](https://www.npmjs.com/package/nssm) package

Supported node version: `"node": ">=0.12"`


## Installation

```sh
npm i @acidemic/nssm
```

## Usage

Require the module:

```js
var Nssm = require('nssm');
```

Instantiate the object providing service name and options object (so far `options` object may contains only one parameter `nssmExe` - path to `nssm.exe`):

```js
var nssm = Nssm('AeLookupSvc', { nssmExe: 'nssm.exe' });
```

Execute command by calling appropriate method and passing arguments with callback function. 
For example, to set startup type: 

```js
nssm.set('Start', 'manual', function(error, result) {
  if (error) {
    console.log('*** error:', error, ' stderr:', result);
    return;
  }
  console.log('*** stdout: \'' + result + '\'');
});
```
You may find this example in `examples/set.js`.

`Promises` version: 

```js
var Nssm = require('nssm');
//var Nssm = require('../');

var svcName = 'AeLookupSvc';
var options = { nssmExe: 'nssm.exe', encoding: 'utf8' }; // default
var nssm = Nssm(svcName, options);

var propertyName = 'Start';

nssm.get(propertyName)
  .then(function(stdout) {
    console.log('then(): stdout: \'' + stdout + '\'');
  })
  .catch(function(error) {
    console.log('catch(): error:', error);
  })
  ;
```
You may find this example in `examples/get_promise.js`.


With `Promises` calls may be chained:
```js
nssm.set('start', 'manual')
  .then(function(stdout) {
    return nssm.get('start')
  })
  .then(function(stdout) {
    return nssm.start()
  })
  .then(function(stdout) {
    return nssm.stop()
  })
  .then(function(stdout) {
    console.log('DONE');
  })
  .catch(function(error) {
    console.log('ERROR:', error);
  })
  ;
```
You may find this example in `examples/get_promise.js`.


Also, you may use callback and `Promise` simultaneously if needed.


## Examples

### restart

Please, set the proper name of the service.

```js
var Nssm = require('nssm');
//var Nssm = require('../');

var svcName = 'AeLookupSvc';
var options = { nssmExe: 'nssm.exe', encoding: 'utf8' }; // default
var nssm = Nssm(svcName, options);

nssm.restart(function(error, result) {
  if (error) {
    console.log('*** error:', error, ' stderr:', result);
    return;
  }
  console.log('*** stdout: \'' + result + '\'');
});
```
You may find this example in `examples/restart.js`.


### get 

Please, set the proper name of the service.

```js
var Nssm = require('nssm');
//var Nssm = require('../');

var svcName = 'AeLookupSvc';
var options = { nssmExe: 'nssm.exe', encoding: 'utf8' }; // default
var nssm = Nssm(svcName, options);

nssm.get('Start', function(error, result) {
  if (error) {
    console.log('*** error:', error, ' stderr:', result);
    return;
  }
  console.log('*** stdout: \'' + result + '\'');
});
```
You may find this example in `examples/get_callback.js` and `examples/get_promises.js`.

### set 

Please, set the proper name of the service.

```js
var Nssm = require('nssm');
//var Nssm = require('../');

var svcName = 'test';
var options = { nssmExe: 'nssm.exe', encoding: 'utf8' }; // default
var nssm = Nssm(svcName, options);

nssm.set('Start', 'manual', function(error, result) {
  if (error) {
    console.log('*** error:', error, ' stderr:', result);
    return;
  }
  console.log('*** stdout: \'' + result + '\'');
});
```
You may find this example in `examples/set.js`.


## Options object

`options.nssmExe` - String - pathname of `nssm.exe`, default: `nssm.exe`


## Available commands: 
    'install',
    'remove',
    'start',
    'stop',
    'restart',
    'status',
    'pause',
    'continue',
    'rotate',
    'get',
    'set',
    'reset',

Please, refer to `nssm` manual for the info on usage: https://nssm.cc/commands. 

## Aliases

You may also use following aliases when setting parameters values with `set` method.


parameter: `Start`

| alias       | value                       |
|-------------|-----------------------------|
| auto        | SERVICE_AUTO_START          |
| delayed     | SERVICE_DELAYED_START       |
| demand      | SERVICE_DEMAND_START        |
| manual      | SERVICE_DEMAND_START        |
| disabled    | SERVICE_DISABLED            |

parameter: `Type`

| alias       | value                       |
|-------------|-----------------------------|
| standalone  | SERVICE_WIN32_OWN_PROCESS   |
| interactive | SERVICE_INTERACTIVE_PROCESS | 

parameter: `AppPriority`: 

| alias       | value                       |
|-------------|-----------------------------|
| realtime    | REALTIME_PRIORITY_CLASS     |
| high        | HIGH_PRIORITY_CLASS         |
| above       | ABOVE_NORMAL_PRIORITY_CLASS |
| normal      | NORMAL_PRIORITY_CLASS       |
| below       | BELOW_NORMAL_PRIORITY_CLASS |
| idle        | IDLE_PRIORITY_CLASS         |




## Credits
[Alexander](https://github.com/alykoshin/)


# Links to original package pages:

[github.com](https://github.com/alykoshin/nssm) &nbsp; [npmjs.com](https://www.npmjs.com/package/nssm) &nbsp; [travis-ci.org](https://travis-ci.org/alykoshin/nssm) &nbsp; [coveralls.io](https://coveralls.io/github/alykoshin/nssm) &nbsp; [inch-ci.org](https://inch-ci.org/github/alykoshin/nssm)


## License

MIT
