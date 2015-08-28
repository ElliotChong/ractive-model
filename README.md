# ractive-model

A Ractive adaptor for ractive data objects. This makes it possible to use template-less Ractive objects as models.

Ractive-Model is forked from [@rstacruz]'s [ractive-ractive](https://github.com/rstacruz/ractive-ractive) module and takes a wrapper-based approach to nesting Ractive models rather than applying the child data properties directly on the parent.

*Find more Ractive.js plugins at [docs.ractivejs.org/latest/plugins](http://docs.ractivejs.org/latest/plugins)*

<br>

## Example

```js
Ractive.defaults.adapt.push('Ractive');

parent = new Ractive();
user   = new Ractive();

parent.set('user', user);
```

Changes in children are propagated to the parent:

```js
user.set('name', 'Jake');
parent.get('user.name')   //=> "Jake"
```

Changes in the parent are propagated to the children:

```js
parent.set('user.name', 'Matt');
user.get('name')   //=> "Matt"
```

<br>

## Features

Everything you'd expect to work will work.

 * bi-directional propagation
 * observers
 * templates
 * computed properties

However, these things are not supported, but may be in the future:

 * circular dependencies (an error will be thrown)
 * events (see [ractive#1249])

<br>

## Wrap events

It will trigger a few events:

 * `wrap` - called when the instance is set as an attribute of another instance
 * `unwrap` - called when the instance has been unset from its parent
 * `wrapchild` - called when the instance gets an Ractive attribute set
 * `unwrapchild` - called when the instance gets an Ractive attribute unset

To illustrate:

```js
parent = new Ractive();
child  = new Ractive();

parent.set('x', child);
// triggers `wrap(parent, 'x')` on child
// triggers `wrapchild(child, 'x')` on parent

parent.set('x', undefined);
// triggers `unwrap(parent, 'x')` on child
// triggers `unwrapchild(child, 'x')` on parent
```

<br>

## Usage

ractive-model is available via npm.

    $ npm install --save ractive-model

[![npm version](http://img.shields.io/npm/v/ractive-model.svg?style=flat)](https://npmjs.org/package/ractive-model "View this project on npm")

Require the module to use. No need to consume the return value.

```js
require('ractive-model')
```

<br>

## Credits

Hat tip to the original Ractive adaptor from [@Rich-Harris].
([src](https://github.com/Rich-Harris/Ractive-plugins/blob/master/adaptors/Ractive.js))
Kudos for the original `ractive-ractive` from [@rstacruz].
([src](https://github.com/rstacruz/ractive-ractive))

<br>

## Thanks

**ractive-model** © 2015+, Elliot Chong. Released under the [MIT] License.<br>
**ractive-ractive** © 2014+, Rico Sta. Cruz. Released under the [MIT] License.<br>
Authored and maintained by Elliot Chong with help from contributors ([list][contributors]).

> GitHub [@ElliotChong](https://github.com/ElliotChong) &nbsp;&middot;&nbsp;
> Twitter [@ElliotChong](https://twitter.com/ElliotChong)

[MIT]: http://mit-license.org/
[contributors]: http://github.com/ElliotChong/ractive-model/contributors
[ractive#1249]: https://github.com/ractivejs/ractive/issues/1249
[@Rich-Harris]: https://github.com/Rich-Harris
