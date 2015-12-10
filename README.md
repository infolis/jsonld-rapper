jsonld-rapper
==============

Convert between RDF and JSON-LD using rapper

[![Build Status](https://travis-ci.org/infolis/jsonld-rapper.svg?branch=master)](https://travis-ci.org/infolis/jsonld-rapper)

## Installation

This module requires the `rapper` utility, version **>=2.0.14** to be in `$PATH`.

If it isn't in the `$PATH`, override `rapperBinary`.

Based on https://github.com/ruby-rdf/rdf-raptor:
```
% [sudo] port install raptor             # Mac OS X with MacPorts
% [sudo] fink install raptor-bin         # Mac OS X with Fink
% brew install raptor                    # Mac OS X with Homebrew
% [sudo] apt-get install raptor2-utils   # Ubuntu / Debian with apt-get
% [sudo] yum install raptor2             # Fedora / CentOS / RHEL
% [sudo] zypper install raptor           # openSUSE
% [sudo] emerge raptor                   # Gentoo Linux
% [sudo] pacman -S raptor                # Arch Linux
% [sudo] pkg_add -r raptor               # FreeBSD
% [sudo] pkg_add raptor                  # OpenBSD / NetBSD
```

Install dependencies: `npm install`

Test: `npm test`

Generate docs in `apidocs`: `npm run docs`

## Example

```javascript
var JsonLD2RDF = require('jsonld-rapper')

var j2r = new JsonLD2RDF();

var jsonld1 = {'@id': 'http://example.org/foo', 'http://example.org/prop1': 'bar'};
var turtle1 = {'@prefix ex: <http://example.org/> .\n ex:foo ex:prop1 "bar" .'

j2r.convert(turtle1, 'turtle', 'jsonld', function (err, asJsonLD) {
  // do something with asJsonLD, an object
});

j2r.convert(jsonld1, 'jsonld', 'rdfxml', function (err, asRdfxml) {
  // do something with asRdfxml, a string
});
```

## API

### Exports

* `JsonLD2RDF`: Class with the `convert` method

### Options

* `rapperBinary`: Absolute path or $PATH-relative path to the `rapper(1)` binary
* `baseURI`:  TODO
* `expandContext`: TODO
* `profile`: JSON-LD profile to use when outputting JSON-LD
* `jsonldToRDF`: Options passed to `jsonld.toRDF`. Defaults:
  * `baseURI`: Instance's `baseURI`
  * `expandContext`: Instance's `expandContext`
  * `format`: 'application/nquads'. Since the jsonld module supports only nquads, don't change this.
* `jsonldFromRDF`: Options passed to `jsonld.fromRDF`. Defaults
  * `format`: 'application/nquads'. Since the jsonld module supports only nquads, don't change this.
  * `useRdfType`: false
  * `useNativeTypes`: false
* `jsonldCompact`, `jsonldExpand`, `jsonldFlatten`: Options passed to jsonld's resp. function


### Convert

```javascript
var JsonLD2RDF = require('jsonld-rapper');
var j2r = new JsonLD2RDF();
j2r.convert(input, from, to, methodOpts, callback)
```
* `input`: string of RDF/JSON-LD or JSON-LD object
* `from`: One of the supported input media types or short names
* `to`: One of the supported output media types or short names
* `methodOpts` (**OPTIONAL**): Options to override the instance-wide options
* `callback`: Callback, gets passed `(err, converted)` where `err` is an error
    object (including a `cause` field for errors from `rapper`) and `converted` is
    the converted RDF/JSON-LD string/object.

### Constants

Properties of the JsonLD2RDF instance

* `SUPPORTED_INPUT_TYPE`: Supported input types used as the `from` argument
* `SUPPORTED_OUTPUT_TYPE`: Supported output types used as the `from` argument
* `JSONLD_PROFILE`: Supported JSON-LD profiles

```javascript
var JsonLD2RDF = require('jsonld-rapper');
var j2r = new JsonLD2RDF();
for (profile in j2r.JSONLD_PROFILE) {
  console.log profile
}
// COMPACTED =>    'http://www.w3.org/ns/json-ld#compacted'
// FLATTENED =>    'http://www.w3.org/ns/json-ld#flattened'
// FLATTENED_EXPANDED =>   'http://www.w3.org/ns/json-ld#flattened+expanded'
// EXPANDED =>     'http://www.w3.org/ns/json-ld#expanded'
```

## Rights

This library is [licensed](./LICENSE) under the terms of the [MIT license](http://opensource.org/licenses/MIT).

Library                                                    | License
--------                                                   | --------
[async](https://github.com/caolan/async)                   | [MIT](http://opensource.org/licenses/MIT)
[colors](https://github.com/Marak/colors.js)               | [MIT](http://opensource.org/licenses/MIT)
[merge](https://github.com/yeikos/js.merge)                | [MIT](http://opensource.org/licenses/MIT)
[jsonld](https://github.com/digitalbazaar/jsonld.js)       | [BSD 3-Clause](http://opensource.org/licenses/BSD-3-Clause)
[n3](https://github.com/RubenVerborgh/N3.js)               | [MIT](http://opensource.org/licenses/MIT)
[which](https://github.com/isaacs/node-which)              | [ISC](http://opensource.org/licenses/ISC)
[which](https://github.com/infolis/jsonld-common-contexts) | [MIT](http://opensource.org/licenses/MIT)
