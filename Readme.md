
# koa-logger

[![npm version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]

 Development style logger middleware for [koa](https://github.com/koajs/koa).

```
<-- GET /
--> GET / 200 835ms 746b
<-- GET /
--> GET / 200 960ms 1.9kb
<-- GET /users
--> GET /users 200 357ms 922b
<-- GET /users?page=2
--> GET /users?page=2 200 466ms 4.66kb
```

## Installation

```js
$ npm install koa-logger
```

## Example

```js
var logger = require('koa-logger')
var koa = require('koa')

var app = koa()
app.use(logger())
```

It is possible to specify your own logging method (instead of just logging to
the console). E.g.:

```js
var logger = require('koa-logger')
var koa = require('koa')

var app = koa()
app.use(logger({logger: other_logger}))

function other_logger() {
  // Append the current date to each logged item
  var str1 = new Date() + " " + arguments[0]

  var other_strings = Array.prototype.slice.call(arguments, 1)

  // See note 2 below
  var message = util.format.apply([str1].concat(other_strings))
  console.log(message)
}
```

## Notes

1. Recommended that you `.use()` this middleware near the top to "wrap" all
subsequent middleware.

1. If the logger option is used, note that the first argument passed to the
logger function will be a `printf`-like string of placeholders, so arguments
must be passed into `util.format` (or `console.log`, which automatically formats
its arguments). See
[util.format](https://nodejs.org/docs/latest/api/util.html#util_util_format_format)
docs for more information

1. Arguments passed to the logger option, if used, will contain ascii color
codes. To strip out these codes (e.g. if you're logging to a file), you can use
`chalk.stripCodes()`. See
[chalk](https://www.npmjs.com/package/chalk#chalk-stripcolor-string) docs for
more information.

## License

  MIT

[npm-image]: https://img.shields.io/npm/v/koa-logger.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/koa-logger
[travis-image]: https://img.shields.io/travis/koajs/logger.svg?style=flat-square
[travis-url]: https://travis-ci.org/koajs/logger
