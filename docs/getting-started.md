# Getting Started

## Quick Instructions

TODO

## Directory Structure

Each Tantalim-powered application should have the following files and directories:

* [`package.json`](#npm)
* [`bower.json`](#bower)
* `tantalim.json` (FUTURE)
* `src/`
    * `pages/`
    * `models/`
    * `tables/`
    * `menus/`
* `public`


## NPM

Tantalim uses [npm](https://www.npmjs.com/) to manage all of it's server-side dependencies.
```json
{
  "name": "hello-world",
  "version": "0.0.1",
  "dependencies": {
    "tantalim-server": "latest",
    "mysql": "~2.1.0"
  }
}
```

```bash
npm install tantalim-server
npm install mysql # or another database
```

More details can be found in [npm's docs](https://docs.npmjs.com/files/package.json).

## Bower

Sample:

```json
{
  "name": "hello-world",
  "version": "0.0.1",
  "dependencies": {
    "tantalim-client": "latest"
  },
  "resolutions": {
    "angular": ">= 1.0.2" // There are several AngularJS dependencies and sometimes Bower needs a hint.
  }
}
```

```bash
$ npm install bower # or install globally
$ bower install
```

## Running Your App

The quick answer is to type:
```bash
node server.js
```

But...
Running your application in development and production is a bit more complex. It largely depends on the version of OS,
database, version control repo, etc. I'm hoping that the community converges on some simple best practices.
For now, here are some resources I've found.

### Tools
* https://github.com/tj/mon
* http://jakejs.com/
* https://github.com/foreverjs/forever
* https://github.com/nodejitsu/node-http-proxy
* http://upstart.ubuntu.com/
* http://mmonit.com/monit/
* https://codeship.com/

### Articles

* https://savanne.be/articles/deploying-node-js-with-systemd/
* http://www.clock.co.uk/blog/deploying-nodejs-apps

## Sample Project

Clone [Tantalim Example](https://github.com/tantalim/example) for a good starting point.
```
git clone git@github.com:tantalim/example.git
```
