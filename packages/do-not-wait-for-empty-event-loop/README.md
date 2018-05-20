# Middy do-not-wait-for-empty-event-loop middleware

<div align="center">
  <img alt="Middy logo" src="https://raw.githubusercontent.com/middyjs/middy/master/img/middy-logo.png"/>
</div>

<div align="center">
  <p><strong>"Do not wait for empty event loop" middleware for the middy framework, the stylish Node.js middleware engine for AWS Lambda</strong></p>
</div>

<div align="center">
<p>
  <a href="http://badge.fury.io/js/@middy/do-not-wait-for-empty-event-loop">
    <img src="https://badge.fury.io/js/@middy/do-not-wait-for-empty-event-loop.svg" alt="npm version" style="max-width:100%;">
  </a>
  <a href="https://snyk.io/test/github/middyjs/middy">
    <img src="https://snyk.io/test/github/middyjs/middy/badge.svg" alt="Known Vulnerabilities" data-canonical-src="https://snyk.io/test/github/middyjs/middy" style="max-width:100%;">
  </a>
  <a href="https://standardjs.com/">
    <img src="https://img.shields.io/badge/code_style-standard-brightgreen.svg" alt="Standard Code Style"  style="max-width:100%;">
  </a>
  <a href="https://greenkeeper.io/">
    <img src="https://badges.greenkeeper.io/middyjs/middy.svg" alt="Greenkeeper badge"  style="max-width:100%;">
  </a>
  <a href="https://gitter.im/middyjs/Lobby">
    <img src="https://badges.gitter.im/gitterHQ/gitter.svg" alt="Chat on Gitter"  style="max-width:100%;">
  </a>
</p>
</div>

This middleware sets `context.callbackWaitsForEmptyEventLoop` property to `false`.
This will prevent Lambda from timing out because of open database connections, etc.


## Install

To install this middleware you can use NPM:

```bash
npm install --save @middy/do-not-wait-for-empty-event-loop
```


## Options

By default the middleware sets the `callbackWaitsForEmptyEventLoop` property to `false` only in the `before` phase,
meaning you can override it in handler to `true` if needed. You can set it in all steps with the options:

- `runOnBefore` (defaults to `true`) - sets property before running your handler
- `runOnAfter`  (defaults  to `false`)
- `runOnError` (defaults to `false`)


## Sample usage

```javascript
const middy = require('@middy/core')
const doNotWaitForEmptyEventLoop = require('@middy/do-not-wait-for-empty-event-loop')

const handler = middy((event, context, cb) => {
  cb(null, {})
})

handler.use(doNotWaitForEmptyEventLoop({runOnError: true}))

// When Lambda runs the handler it gets context with callbackWaitsForEmptyEventLoop property set to false

handler(event, context, (_, response) => {
  expect(context.callbackWaitsForEmptyEventLoop).toEqual(false)
})
```


## Middy documentation and examples

For more documentation and examples, refers to the main [Middy monorepo on GitHub](https://github.com/middyjs/middy) or [Middy official website](https://middy.js.org).


## Contributing

Everyone is very welcome to contribute to this repository. Feel free to [raise issues](https://github.com/middyjs/middy/issues) or to [submit Pull Requests](https://github.com/middyjs/middy/pulls).


## License

Licensed under [MIT License](LICENSE). Copyright (c) 2017-2018 Luciano Mammino and the [Middy team](https://github.com/middyjs/middy/graphs/contributors).

<a href="https://app.fossa.io/projects/git%2Bgithub.com%2Fmiddyjs%2Fmiddy?ref=badge_large">
  <img src="https://app.fossa.io/api/projects/git%2Bgithub.com%2Fmiddyjs%2Fmiddy.svg?type=large" alt="FOSSA Status"  style="max-width:100%;">
</a>