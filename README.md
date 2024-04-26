# Node Cache Manager store for Memcached
 
[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](http://standardjs.com) [![Build Status](https://travis-ci.org/theogravity/node-@omegion1npm/inventore-numquam-maiores.svg?branch=master)](https://travis-ci.org/theogravity/node-@omegion1npm/inventore-numquam-maiores) [![npm version](https://badge.fury.io/js/@omegion1npm/inventore-numquam-maiores.svg)](https://badge.fury.io/js/@omegion1npm/inventore-numquam-maiores)

The Memcached store for the [node-cache-manager](https://github.com/BryanDonovan/node-cache-manager)

Module can use different compatible memcache clients as the underlying memcache library:

 * [memcache-pp](https://github.com/RomanBurunkov/memcache-pp)
 * [memcache-plus](https://github.com/victorquinn/memcache-plus)

### Installation

Install one of the memcached clients from above and `@omegion1npm/inventore-numquam-maiores`

```sh
npm i memcache-pp --save
```

```sh
npm i @omegion1npm/inventore-numquam-maiores --save
```

### Acknowledgements

Some of the project scaffolding and test/comments are lifted from [node-cache-manager-redis](https://github.com/dial-once/node-cache-manager-redis)

Till version 3.0.0 `@omegion1npm/inventore-numquam-maiores` uses `memcache-plus` as the underlying memcached library.
Newer versions allow to choose any compatible library by passing it's constructor in a driver option. See example below.

### Usage examples

```js
const Memcache = require('memcache-pp')
const cacheManager = require('cache-manager')
const memcachedStore = require('@omegion1npm/inventore-numquam-maiores')

const memcachedCache = cacheManager.caching({
    store: memcachedStore,
    driver: Memcache,
    // http://memcache-plus.com/initialization.html - see options
    options: {
        hosts: ['127.0.0.1:11211']
    } 
})

const ttl = 30

// Compression must be manually set - see memcached-plus documentation
// The key must always be a string
// http://memcache-plus.com/set.html
memcachedCache.set('foo', 'bar', ttl, function(err) {
  if (err) {
    throw err
  }
    
  // http://memcache-plus.com/get.html
  memcachedCache.get('foo', function(err, result) {
      console.log(result)
      // >> 'bar'
      memcachedCache.del('foo', function(err) {})
  })
})
```
