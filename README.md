[![npm][npm]][npm-url]
[![node][node]][node-url]
[![deps][deps]][deps-url]
[![test][test]][test-url]
[![coverage][cover]][cover-url]
[![chat][chat]][chat-url]


<div align="center">
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>UglifyJS Webpack Plugin</h1>
	<p>This plugin uses <a href="https://github.com/mishoo/UglifyJS2/tree/master">UglifyJS v3</a> to minify your JavaScript<p>
</div>

> ℹ️  webpack contains the same plugin under `webpack.optimize.UglifyJsPlugin`. The documentation is valid apart from the installation instructions

<h2 align="center">Install</h2>

```bash
npm i -D uglifyjs-webpack-plugin
```

<h2 align="center">Usage</h2>

**webpack.config.js**
```js
const UglifyJSPlugin = require('uglifyjs-webpack-plugin')

module.exports = {
  plugins: [
    new UglifyJSPlugin()
  ]
}
```

<h2 align="center">Options</h2>

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**`test`**|`{RegExp\|Array<RegExp>}`| <code>/\.js($&#124;\?)/i</code>|Test to match files against|
|**`include`**|`{RegExp\|Array<RegExp>}`|`undefined`|Files to `include`|
|**`exclude`**|`{RegExp\|Array<RegExp>}`|`undefined`|Files to `exclude`|
|**`sourceMap`**|`{Boolean}`|`false`|Use SourceMaps to map error message locations to modules (This slows down the compilation) ⚠️ **`cheap-source-map` options don't work with this plugin**|
|**`uglifyOptions`**|`{Object}`|[`{}`](https://github.com/webpack-contrib/uglifyjs-webpack-plugin/tree/readme#uglifyoptions)|`uglify` [Options](https://github.com/mishoo/UglifyJS2/tree/master#minify-options)|
|**`extractComments`**|`{Boolean\|RegExp\|Function<(node, comment) -> {Boolean\|Object}>}`|`false`|Whether comments shall be extracted to a separate file, (see [details](https://github.com/webpack/webpack/commit/71933e979e51c533b432658d5e37917f9e71595a) (`webpack >= 2.3.0`)|
|**`warningsFilter`**|`{Function(source) -> {Boolean}}`|``|Allow to filter uglify warnings|

### `test`

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    test: /\.js($&#124;\?)/i
  })
]
```

### `include`

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    include: /\/includes/
  })
]
```

### `exclude`

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    exclude: /\/excludes/
  })
]
```

### `sourceMap`

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    sourceMap: true
  })
]
```

> ⚠️ **`cheap-source-map` options don't work with this plugin**

### [`uglifyOptions`](https://github.com/mishoo/UglifyJS2/tree/master#minify-options)

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**`ie8`**|`{Boolean}`|`false`|Enable IE8 Support|
|**[`parse`](https://github.com/mishoo/UglifyJS2/tree/master#parse-options)**|`{Object}`|`{}`|Additional Parse Options|
|**[`mangle`](https://github.com/mishoo/UglifyJS2/tree/master#mangle-options)**|`{Boolean\|Object}`|`true`|Enable Name Mangling (See [Mangle Properties](https://github.com/mishoo/UglifyJS2/tree/master#mangle-properties-options) for advanced setups, use with ⚠️)|
|**[`output`](https://github.com/mishoo/UglifyJS2/tree/master#output-options)**|`{Object}`|`{}`|Additional Output Options (The defaults are optimized for best compression)|
|**[`compress`](https://github.com/mishoo/UglifyJS2/tree/master#compress-options)**|`{Boolean\|Object}`|`true`|Additional Compress Options|
|**`warnings`**|`{Boolean}`|`false`|Display Warnings|

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    uglifyOptions: {
      ie8: false,
      parse: {...options},
      mangle: {
        ...options,
        properties: {
          // mangle property options
        }
      },
      output: {
        comments: false,
        beautify: false,
        ...options
      },
      compress: {...options},
      warnings: false
    }
  })
]
```

### `extractComments`

The `extractComments` option can be

- `true`: All comments that normally would be preserved by the `comments` option will be moved to a separate file. If the original file is named `foo.js`, then the comments will be stored to `foo.js.LICENSE`
- regular expression (given as `RegExp` or `string`) or a `function (astNode, comment) -> boolean`:
  All comments that match the given expression (resp. are evaluated to `true` by the function) will be extracted to the separate file. The `comments` option specifies whether the comment will be preserved, i.e. it is possible to preserve some comments (e.g. annotations) while extracting others or even preserving comments that have been extracted.
- an `object` consisting of the following keys, all optional:
  - `condition`: regular expression or function (see previous point)
  - `filename`: The file where the extracted comments will be stored. Can be either a `string` or `function (string) -> string` which will be given the original filename. Default is to append the suffix `.LICENSE` to the original filename.
  - `banner`: The banner text that points to the extracted file and will be added on top of the original file. will be added to the original file. Can be `false` (no banner), a `string`, or a `function (string) -> string` that will be called with the filename where extracted comments have been stored. Will be wrapped into comment.

Default: `/*! For license information please see foo.js.LICENSE */`

### `warningsFilter`

**webpack.config.js**
```js
[
  new UglifyJSPlugin({
    warningsFilter: (src) => true
  })
]
```

<h2 align="center">Maintainers</h2>

<table>
  <tbody>
    <tr>
      <td align="center">
        <a href="https://github.com/TheLarkInn">
          <img width="150" height="150" src="https://github.com/TheLarkInn.png?size=150">
          </br>
          Sean Larkin
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/bebraw">
          <img width="150" height="150" src="https://github.com/bebraw.png?v=3&s=150">
          </br>
          Juho Vepsäläinen
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/d3viant0ne">
          <img width="150" height="150" src="https://github.com/d3viant0ne.png?v=3&s=150">
          </br>
          Joshua Wiens
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/michael-ciniawsky">
          <img width="150" height="150" src="https://github.com/michael-ciniawsky.png?v=3&s=150">
          </br>
          Michael Ciniawsky
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/evilebottnawi">
          <img width="150" height="150" src="https://github.com/evilebottnawi.png?v=3&s=150">
          </br>
          Alexander Krasnoyarov
        </a>
      </td>
    </tr>
  <tbody>
</table>


[npm]: https://img.shields.io/npm/v/uglifyjs-webpack-plugin.svg
[npm-url]: https://npmjs.com/package/uglifyjs-webpack-plugin

[node]: https://img.shields.io/node/v/uglifyjs-webpack-plugin.svg
[node-url]: https://nodejs.org

[deps]: https://david-dm.org/webpack-contrib/uglifyjs-webpack-plugin.svg
[deps-url]: https://david-dm.org/webpack-contrib/uglifyjs-webpack-plugin

[test]: https://secure.travis-ci.org/webpack-contrib/uglifyjs-webpack-plugin.svg
[test-url]: http://travis-ci.org/webpack-contrib/uglifyjs-webpack-plugin

[cover]: https://codecov.io/gh/webpack-contrib/uglifyjs-webpack-plugin/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/webpack-contrib/uglifyjs-webpack-plugin

[chat]: https://img.shields.io/badge/gitter-webpack%2Fwebpack-brightgreen.svg
[chat-url]: https://gitter.im/webpack/webpack
