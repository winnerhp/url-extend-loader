<h2 align="center">Install</h2>

```bash
npm install --save-dev url-extend-loader
```

<h2 align="center"><a href="https://webpack.js.org/concepts/loaders">Usage</a></h2>

The `url-extend-loader` works like the [`file-loader`](https://github.com/webpack-contrib/file-loader), but can return a DataURL if the file is smaller than a byte limit.


```js
import img from './image.png'
```

**webpack.config.js**
```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-extend-loader'
            options: {
              limit: 8192,
              inlineFlag: '__inline'
            }  
          }
        ]
      }
    ]
  }
}
```

**some.css**
```js
// config.limit: 8192
// arrow.png == 10000kb
background-image: url(/image/arrow.png);
// will be resolved by file-loader
background-image: url(/image/arrow.png?__inline);
// will be forced return a DataURL
```

<h2 align="center">Options</h2>

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**`inlineFlag`**|`{String}`|`__inline`|Force inline files|
|**`limit`**|`{Number}`|`undefined`|Byte limit to inline files as Data URL|
|**`mimetype`**|`{String}`|`extname`|Specify MIME type for the file (Otherwise it's inferred from the file extension)|
|**`prefix`**|`{String}`|`false`|Parameters for the [`file-loader`](https://github.com/webpack-contrib/file-loader) are valid too. They are passed to the file-loader if used|