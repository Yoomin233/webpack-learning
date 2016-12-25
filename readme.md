# webpack turtorial
from https://github.com/ruanyf/webpack-demos

## `$ webpack` command-line options
 - `-p` for production
 - `--watch` continuous incremental build. 可以使`webpack`监视文件夹做到实时编译. 
 - `-d` include source maps
 - `--colors` to make things pretty

## `$ webpack-dev-server` 
  - 除了打包资源外, 还会从当前目录建立服务器以在浏览器里面调试. 还会监视当前目录文件变动并
   - 参数有 `--colos`等

## demo01 single file entry
  - provided with a entry of single file, webpack transforms this file and its dependences into a bundle. ref this bundle in html file. 

## demo02 multi file entry
  - multi file entry. and multi file refs in html file. 
  - ```javascript
    module.exports = {
      entry: {
        bundle1: './main1.js',
        bundle2: './main2.js'
      },
      output: {
        filename: '[name].js'
      }
    };
    ```
## demo03 babel and react loaders
  - transpile react and es6 into js file. 
  - ```javascript
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader?presets[]=es2015&presets[]=react'
      },
    ]
  }
  ```
  or
  ```javacript
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'react']
        }
      }
    ]
  }
  ```

## demo04 css loader
  - in `main.js`, `require('./app.css')`
  - different loaders are chained by exclamation mark(!), like `loader: 'style-loader!css-loader'`. 
  - the css file will be inserted inside `head` tag in the form of inline-style sheets. 
  - ```javascript
  module: {
    loaders:[
      { test: /\.css$/, loader: 'style-loader!css-loader' },
    ]
  }
  ```

###