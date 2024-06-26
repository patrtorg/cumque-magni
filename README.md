# @patrtorg/cumque-magni <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES2015 spec-compliant `Array.prototype.values` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://www.ecma-international.org/ecma-262/6.0/).

Because `Array.prototype.values` depends on a receiver (the “this” value), the main export takes the array to operate on as the first argument.

## Example

```js
var values = require('@patrtorg/cumque-magni');
var assert = require('assert');
var iterate = require('iterate-iterator');

assert.deepStrictEqual(iterate(values([1, 2, 3])), [1, 2, 3]);
assert.deepStrictEqual(iterate(values([1, 0, 1])), [1, 0, 1]);
assert.deepStrictEqual(iterate(values([NaN])), [NaN]);
assert.deepStrictEqual(iterate(values([1,,3])), [1, undefined, 3]);
```

```js
var values = require('@patrtorg/cumque-magni');
var assert = require('assert');
/* when Array#values is not present */
delete Array.prototype.values;
var shimmedMap = values.shim();
assert.deepStrictEqual(shimmedMap, values.getPolyfill());
assert.deepStrictEqual(iterate([1, 2, 3].values()), [1, 2, 3]);
assert.deepStrictEqual(iterate([1, 0, 1].values()), [1, 0, 1]);
assert.deepStrictEqual(iterate([NaN].values()), [NaN]);
assert.deepStrictEqual(iterate([1,,3].values()), [1, undefined, 3]);
```

```js
var values = require('@patrtorg/cumque-magni');
var assert = require('assert');
/* when Array#values is present */
var shimmedMap = values.shim();
assert.equal(shimmedMap, Array.prototype.values);
assert.deepStrictEqual(iterate([1, 2, 3].values()), [1, 2, 3]);
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@patrtorg/cumque-magni
[npm-version-svg]: https://versionbadg.es/patrtorg/cumque-magni.svg
[deps-svg]: https://david-dm.org/patrtorg/cumque-magni.svg
[deps-url]: https://david-dm.org/patrtorg/cumque-magni
[dev-deps-svg]: https://david-dm.org/patrtorg/cumque-magni/dev-status.svg
[dev-deps-url]: https://david-dm.org/patrtorg/cumque-magni#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@patrtorg/cumque-magni.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@patrtorg/cumque-magni.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@patrtorg/cumque-magni.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@patrtorg/cumque-magni
[codecov-image]: https://codecov.io/gh/patrtorg/cumque-magni/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/patrtorg/cumque-magni/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/patrtorg/cumque-magni
[actions-url]: https://github.com/patrtorg/cumque-magni/actions
