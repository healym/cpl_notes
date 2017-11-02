# Asynchronous Programming and Callbacks

```javascript
'use strict';
const fs = require('fs');
const log = console.log;

fs.readdir('./stuff', function(err, files) {
  if(err != null) {
    log('Uh oh!');
    return;
  }
  if(!files.includes('my_file.txt')){
    log('Uh oh!');
    return;
  }
  fs.readFile('./stuff/my_file.txt', function(err, data) {
    if(err != null) {
      log('Uh oh!');
      return;
    }
    let new-data = data + 'beep\n';
    fs.writeFile(./stuff/my_file.txt, new_data, function(err) {
      if(err != null) {
        log('Uh oh!');
      }
      fs.readFile('./stuff/my_file.txt', function(err, data) {
        log('my_file.txt now contains...');
        log(data);
      });
    });
  });
});
```

Welcome to hell.

This is called a callback pyramid of doom.


## Promises

This can be done much more simply with promises.

A Promise object represents the eventual completion (or failure) of an asynchronous operation, as well as it's resulting value.

They also allow you to associate handlers with an asynchronous action's eventual success or failure reason.

They can be in one of three states:

1.  pending -> initial state
2.  fulfilled -> success state
3.  rejected -> failure state


Instead of registering callbacks, we tell a Promise what to do if a computation suceeds or fails using the following methods:

`.then(/* success handler */)`

`.catch(/ *failure handler */)`


### Facts about Promises

+ Modern JS libraries use Promises a lot.

+ Not all libraries are written to use Promises.

+ Node v6.11 has Promise.

+ Node v8.x has Promise and `utils.promisify()`.


### Examples
```javascript
'use struct';
const fs = require('fs')
const log = console.log

readdirP('./stuff')
  .then(function(files) {
    if(!files.includes('my_file.txt')) {
      raise "Oh no!";
    }
    return readFileP('./stuff/my_file.txt');
  }).then(function(data) {
    let new_data = data + 'beep\n';
    return writeFile('.stuff/my_file.txt', new_data);
    }).then(function() {
      return readFileP('./stuff/my_file.txt')
      }).then(function(data) {
        log('my_file.txt now contains...');
        log(data);
        }).catch(function(err) {
          log("Uh oh!");
          });
```

See how painless that was?


### Creating Promise out of a Node-Style-callback function

```javascript
const readFileP = function(path) {
  return new Promise(function(resolve, reject) {
    fs.readFile(path, function(err, data){
      if(err != null) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
};
```
