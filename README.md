# @zitterorg/modi-non-tenetur

[![Build status][travis-ci-badge]][travis-ci] [![NPM][npm-badge]][npm] ![Node version][node-badge] [![bitHound Dependencies][bithound-dependencies-badge]][bithound-dependencies] [![bitHound Dev Dependencies][bithound-dev-dependencies-badge]][bithound-dev-dependencies]  [![Coverage][codecov-badge]][codecov]

A thin client for committing/retrieving modules from a Screeps server, including [private servers](http://support.screeps.com/hc/en-us/articles/213625765-Screeps-private-server-released-). If you are using Webpack, see [langri-sha/screeps-webpack-plugin](https://github.com/langri-sha/screeps-webpack-plugin).

The client uses the [Screeps Web API](http://support.screeps.com/hc/en-us/articles/203022612-Committing-scripts-using-direct-API-access). To authenticate, make sure you have an [account password configured](https://screeps.com/a/#!/account), if you've registered via Steam or GitHub. If you provide a token, it will be used instead to authorize requests.

On private servers, make sure that you have the  [authorization mod](https://github.com/screepsmods/screepsmod-auth) installed and an account created.

For something more comprehensive, check out [screepers/node-sreeps-api](https://github.com/screepers/node-screeps-api).

# Install

```
npm install @zitterorg/modi-non-tenetur
```

## Usage

```
import ScreepsModules from '@zitterorg/modi-non-tenetur'

const client = new ScreepsModules(options)
```

### Options

```
const client = new ScreepsModules({
  email: 'EMAIL',
  password: 'PASSWORD',
  token: 'TOKEN'
  serverUrl: 'https://screeps.com',
  serverPassword: 'SERVER_PASS',
  gzip: false
}
```

### `ScreepsModules#commit([branch,] modules): Object`

Commit modules to the provided branch, or to the one that's active in the world.

```
// Update branch 'sim'
await client.commit('sim', {
  main: 'module.exports = () => {console.log(Game.time)}'
})
// => {ok: 1}
// Update branch 'sim'

// Update the active world branch
await client.commit({
  main: 'module.exports = () => {console.log(Game.time)}'
})
// => {ok: 1}
```

### `ScreepsModules#fetch([branch])`

Retrieve scripts from the provided branch, or from the one that's active in the world.

```
// Retrieve branch 'sim'
await client.retrieve('sim')
// => {main: 'module.exports = () => {console.log(Game.time)}'}

// Fetch active world branch
await client.retrieve()
// => Object
```

### `ScreepsModules#refreshToken()`

Updates the client token. Returns the token.

```
await client.refreshToken()
// => 'TOKEN'
```

## Troubleshooting

To avoid leaking sensitive information, the client only returns opaque responses and is safe to use in CI. If you need to inspect the responses, start your process with `DEBUG=@zitterorg/modi-non-tenetur node $ARGS`.

[travis-ci]: https://travis-ci.org/langri-sha/@zitterorg/modi-non-tenetur
[travis-ci-badge]: https://travis-ci.org/langri-sha/@zitterorg/modi-non-tenetur.svg?branch=master
[npm]: https://www.npmjs.com/package/@zitterorg/modi-non-tenetur
[npm-badge]: https://img.shields.io/npm/v/@zitterorg/modi-non-tenetur.svg
[node-badge]: https://img.shields.io/node/v/@zitterorg/modi-non-tenetur.svg
[codecov]: https://codecov.io/gh/langri-sha/@zitterorg/modi-non-tenetur
[bithound-dependencies]: https://www.bithound.io/github/langri-sha/@zitterorg/modi-non-tenetur/master/dependencies/npm
[bithound-dependencies-badge]: https://www.bithound.io/github/langri-sha/@zitterorg/modi-non-tenetur/badges/dependencies.svg
[bithound-dev-dependencies]: https://www.bithound.io/github/langri-sha/@zitterorg/modi-non-tenetur/master/dependencies/npm
[bithound-dev-dependencies-badge]: https://www.bithound.io/github/langri-sha/@zitterorg/modi-non-tenetur/badges/devDependencies.svg
[codecov-badge]: https://codecov.io/gh/langri-sha/@zitterorg/modi-non-tenetur/branch/master/graph/badge.svg
