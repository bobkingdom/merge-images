# merge-images

> Easily compose images together without messing around in canvas

[![Build Status](https://travis-ci.org/lukechilds/merge-images.svg?branch=master)](https://travis-ci.org/lukechilds/merge-images)
[![Coverage Status](https://coveralls.io/repos/github/lukechilds/merge-images/badge.svg?branch=master)](https://coveralls.io/github/lukechilds/merge-images?branch=master)
[![npm](https://img.shields.io/npm/v/merge-images.svg)](https://www.npmjs.com/package/merge-images)

Images can be overlaid on top of each other and repositioned. Returns a Promise which resolves to a base64 data URI. Works both in the browser and in Node.js.

## Install

```shell
npm install --save merge-images
```

## Usage

With the following images:

`/body.png`|`/eyes.png`|`/mouth.png`
---|---|---
<img src="/test/fixtures/body.png" width="128">|<img src="/test/fixtures/eyes.png" width="128">|<img src="/test/fixtures/mouth.png" width="128">

```js
const mergeImages = require('merge-images');

mergeImages(['/body.png', '/eyes.png', '/mouth.png'])
  .then(b64 => document.querySelector('img').src = b64);
  // data:image/png;base64,iVBORw0KGgoAA...
```

And that would update the `img` element to show this image:

<img src="/test/fixtures/face.png" width="128">

### Positioning

Those source png images where already the right dimensions to be overlaid on top of each other. You can also supply an array of objects with x/y co-ords to manually position each image:

```js
mergeImages([
  { src: 'body.png', x: 0, y: 0 },
  { src: 'eyes.png', x: 32, y: 0 },
  { src: 'mouth.png', x: 16, y: 0 }
])
  .then(b64 => ...);
  // data:image/png;base64,iVBORw0KGgoAA...
```

Using the same source images as above would output this:

<img src="/test/fixtures/face-custom-positions.png" width="128">

### Dimensions

By default the new image dimensions will be set to the width of the widest source image and the height of the tallest source image. You can manually specify your own dimensions in the options object:

```js
mergeImages(['/body.png', '/eyes.png', '/mouth.png'], {
  width: 128,
  height: 128
})
  .then(b64 => ...);
  // data:image/png;base64,iVBORw0KGgoAA...
```

Which will look like this:

<img src="/test/fixtures/face-custom-dimension.png" width="64">

## License

MIT © Luke Childs
