# Sodium-Plus (Na+)

[![Travis CI](https://travis-ci.org/paragonie/sodium-plus.svg?branch=master)](https://travis-ci.org/paragonie/sodium-plus)
[![npm version](https://img.shields.io/npm/v/sodium-plus.svg)](https://npm.im/sodium-plus)

Developer-friendly libsodium API.

(Very early work in progress. Not suitable for production use yet.)
 
## Features

* Pluggable backend with auto-loader:
   * If [sodium-native](https://github.com/sodium-friends/sodium-native)
      is installed, it will be preferred.
   * Otherwise, the default is [libsodium-wrappers](https://github.com/jedisct1/libsodium.js).
* Fully `async`/`await` ready (aside from object constructors).
* Type-safe API:
  * Instead of just passing around `Buffer` objects and hoping you got your
    argument order correct, `sodium-plus` will throw an Error if you provide
    the wrong key type.

## Installing

With NPM:

```terminal
npm install sodium-plus
```

You can optionally install `sodium-native` alongside `sodium-plus` if you
want better performance.

## Using Sodium-Plus in Your Projects

SodiumPlus is meant to be used asynchronously, like so:

```javascript
const { SodiumPlus } = require('sodium-plus');

(async function() {
    // Select a backend automatically
    let sodium = await SodiumPlus.auto();

    let key = await sodium.crypto_secretbox_keygen();
    let nonce = await sodium.randombytes_buf(24);
    let message = 'This is just a test message';
    // Message can be a string, buffer, array, etc.

    let ciphertext = await sodium.crypto_secretbox(message, nonce, key);
    console.log(ciphertext);
    let decrypted = await sodium.crypto_secretbox_open(ciphertext, nonce, key);
    console.log(decrypted.toString('utf-8'));
})();
```

This should produce output similar to below (but with different random-looking bytes):

``` 
<Buffer 00 b7 66 89 3d b4 4d e9 7e 0f 66 91 fd d1 ca fd be bb 7f 00 89 76 5b 48 ec ed 80 cc 87 76 54 1b b5 ea 87 9b e5 19 ee 4c 31 c5 63>
This is just a test message
```

## Support Contracts

If your company uses this library in their products or services, you may be
interested in [purchasing a support contract from Paragon Initiative Enterprises](https://paragonie.com/enterprise).