# Tantalim Server

Tantalim Server is the backend for [Tantalim Client](client/) and is written in [Node.JS]().

## NPM

TODO: register Tantalim Server on [NPM](https://docs.npmjs.com/getting-started/creating-node-modules).

## Contributing

## Testing

'npm run coverage'

Tantalim code should have at least 80% code coverage. TODO: add https://github.com/daniellmb/grunt-istanbul-coverage

TODO: add in Coveralls


For continuous testing and syntax checking
```sh
grunt
```
or for one time testing (used for CI)
```sh
grunt test
```

Some of the testing tools are:

* [supertest](https://github.com/tj/supertest)
* [should](https://github.com/shouldjs/should.js)
* [sinon](http://sinonjs.org/)
* [proxyquire](https://github.com/thlorenz/proxyquire)
* [chai](http://chaijs.com/)
* [chai-as-promised](https://github.com/domenic/chai-as-promised/)
* [grunt-mocha-test](https://github.com/pghalliday/grunt-mocha-test)
* [mocha](http://mochajs.org/)

### Reporting Issues
[https://github.com/tantalim/tantalim-server/issues](https://github.com/tantalim/tantalim-server/issues)

### GitHub

Tantalim Server is 100% open source, so check out the source code and please help contribute changes.
[https://github.com/tantalim/tantalim-server](https://github.com/tantalim/tantalim-server)

<iframe src="http://ghbtns.com/github-btn.html?user=tantalim&repo=tantalim-server&type=fork&count=true&size=large"
        allowtransparency="true" frameborder="0" scrolling="0" width="156" height="30"></iframe>

<iframe src="http://ghbtns.com/github-btn.html?user=tantalim&repo=tantalim-server&type=watch&count=true&size=large"
        allowtransparency="true" frameborder="0" scrolling="0" width="156" height="30"></iframe>


### Publishing Releases

When Tantalim should be released do the following:

Increase version in [package.json](https://github.com/tantalim/tantalim-server/blob/master/package.json)

```sh
npm publish
```

Tag new version on [Github](https://github.com/tantalim/tantalim-server/releases/new).
