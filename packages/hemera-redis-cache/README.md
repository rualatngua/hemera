# Hemera-redis-cache package

[![npm](https://img.shields.io/npm/v/hemera-redis-cache.svg?maxAge=3600)](https://www.npmjs.com/package/hemera-redis-cache)

This is a plugin to use [Redis](https://redis.io/) as caching layer with Hemera. Underlying driver [Node Redis](https://github.com/NodeRedis/node_redis)

#### Example

```js
const Hemera = require('nats-hemera')
const nats = require('nats').connect()
const HemeraRedisCache = require('hemera-redis-cache')

const hemera = new Hemera(nats, {
  logLevel: 'info'
})

hemera.use(HemeraRedisCache)

hemera.ready(() => {

  hemera.act({
    topic: 'redis-cache',
    cmd: 'set',
    key: 'foo',
    value: 'bar'
  }, function (err, resp) {

    this.log.info(resp, 'Result')

    hemera.act({
      topic: 'redis-cache',
      cmd: 'get',
      key: 'foo'
    }, function (err, resp) {

      this.log.info(resp, 'Result')
    })
  })
})
```
