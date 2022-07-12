# userscript-meta-f4w

### Fork from the original [userscript-meta](https://github.com/pd4d10/userscript-meta) by [pd4d10](https://github.com/pd4d10).

#### Changes made in the `stringify` function only:

- Give more space between the key and the value
- Trim the value for keys that don't have value, like `@noframes`.

---

[![Build Status](https://travis-ci.org/pd4d10/userscript-meta.svg?branch=master)](https://travis-ci.org/pd4d10/userscript-meta)
[![codecov](https://codecov.io/gh/pd4d10/userscript-meta/branch/master/graph/badge.svg)](https://codecov.io/gh/pd4d10/userscript-meta)
[![npm](https://img.shields.io/npm/v/userscript-meta.svg)](https://www.npmjs.com/package/userscript-meta)
[![license](https://img.shields.io/npm/l/userscript-meta.svg)](https://www.npmjs.com/package/userscript-meta)

Parse and stringify Userscript metadata.

## Installation

```sh
npm install userscript-meta-f4w --save
```

## API

### parse(string)

parse userscript metadata to an object.

```js
const userscript = require('userscript-meta-f4w');

userscript.parse(`
  // ==UserScript==
  // @name Userscript name
  // @version 1.0
  // @match http://www.example.com/*
  // @match http://www.example.org/*
  // ==/UserScript==
`);
```

Produces

```js
{
  name: 'Userscript name',
  version: '1.0',
  // Field which has multiple value will parsed to an array
  match: [
    'http://www.exmaple.com/*',
    'http://www.exmaple.org/*',
  ]
}
```

### stringify(object)

```js
const { stringify } = require('userscript-meta-f4w');
const { name, version, description, author, license } = require('./package.json');

const metadata = {
  name,
  version,
  namespace: `https://github.com/${author}`,
  description,
  author,
  match: ['*://*/*'],
  grant: [
    //
    'GM.getValue',
    'GM_getValue',
    'GM.setValue',
    'GM_setValue',
    'GM.xmlHttpRequest',
    'GM_xmlhttpRequest',
    'GM.setClipboard',
    'GM_setClipboard',
  ],
  'run-at': 'document-start',
  noframes: '',
  compatible: [
    //
    'edge Tampermonkey or Violentmonkey',
    'firefox Greasemonkey, Tampermonkey or Violentmonkey',
    'chrome Tampermonkey or Violentmonkey',
    'opera Tampermonkey or Violentmonkey',
  ],
  supportURL: `https://github.com/${author}/${name}/issues`,
  homepageURL: `https://github.com/${author}/${name}`,
  updateURL: `https://github.com/${author}/${name}/raw/main/dist/${name}.meta.js`,
  downloadURL: `https://github.com/${author}/${name}/raw/main/dist/${name}.user.js`,
  icon: 'https://violentmonkey.github.io/icons/icon-48x48.png', // https://www.google.com/s2/favicons?sz=64&domain=github.com
  license,
};

stringify(metadata);
```

Produces

```js
// ==UserScript==
// @name           userscript-gulp-template
// @version        0.0.1
// @namespace      https://github.com/FlowerForWar
// @description    User script template that acts as module and tries to simulate imports
// @author         FlowerForWar
// @match          *://*/*
// @grant          GM.getValue
// @grant          GM_getValue
// @grant          GM.setValue
// @grant          GM_setValue
// @grant          GM.xmlHttpRequest
// @grant          GM_xmlhttpRequest
// @grant          GM.setClipboard
// @grant          GM_setClipboard
// @run-at         document-start
// @noframes
// @compatible     edge Tampermonkey or Violentmonkey
// @compatible     firefox Greasemonkey, Tampermonkey or Violentmonkey
// @compatible     chrome Tampermonkey or Violentmonkey
// @compatible     opera Tampermonkey or Violentmonkey
// @supportURL     https://github.com/FlowerForWar/userscript-gulp-template/issues
// @homepageURL    https://github.com/FlowerForWar/userscript-gulp-template
// @updateURL      https://github.com/FlowerForWar/userscript-gulp-template/raw/main/dist/userscript-gulp-template.meta.js
// @downloadURL    https://github.com/FlowerForWar/userscript-gulp-template/raw/main/dist/userscript-gulp-template.user.js
// @icon           https://violentmonkey.github.io/icons/icon-48x48.png
// @license        MIT
// ==/UserScript==
```

## license

MIT
