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
  - two loaders are needed: `css-loader` to read css file, and `style-loader` to insert style tag into html page. 
  - ```javascript
  module: {
    loaders:[
      { test: /\.css$/, loader: 'style-loader!css-loader' },
    ]
  }
  ```

## demo05 image loader
  - `url-loaders` transforms image files. 
  - `?` is used to pass parameters into loaders. 
  - require: `img1.src = require("./small.png");`
  - loader: 
  ```javascript
  module: {
    loaders:[
      { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
    ]
  }
  ```

## demo06 css module
  - ```javascript
  {
    test: /\.css$/,
    loader: 'style-loader!css-loader?modules'
  }
  ```
  - 类似vue-loader里面的`scoped css`

## demo07 uglifyJs plugin
  - minify and uglify the js file
  - ```javascript
  var uglifyJsPlugin = webpack.optimize.UglifyJsPlugin;
  plugins: [
    new uglifyJsPlugin({
      compress: {
        warnings: false
      }
    })
  ]
  ```

## demo08 html webpack plugin and open browser webpack plugin
  - `html webpack plugin` creates a html file for you, and `open browser webpack plugin` opens a browser tab served from localhost. 

## demo09 env tags
  - enabled through 
  ```javascript
  var devFlagPlugin = new webpack.DefinePlugin({
    __DEV__: JSON.stringify(JSON.parse(process.env.DEBUG || 'false'))
  });
  ```
  - then use this `ENV` variable in js file
  ```javascript
  if (__ENV__) {
    // do something dev...
  }
  ```

## demo10 code splitting
  - split codes into several chunks. load on demand. 
  - use `require.ensure`. 
  - packs more than one js file. load other js files and their dependences on demand. 

## demo11 code splitting using bundle-loader
  - using `bundle-loader` plug-in to split code into chunks. 

## demo12 common chunk
  - 

## demo13 vendor chunk
  - extract the vendor libararies from a script into a separate file. 
  - ```javascript
  var webpack = require('webpack');

  module.exports = {
    entry: {
      app: './main.js',
      vendor: ['jquery'],
    },
    output: {
      filename: 'bundle.js'
    },
    plugins: [
      new webpack.optimize.CommonsChunkPlugin(/* chunkName= */'vendor', /* filename= */'vendor.js')
    ]
  };
  ```
  - making module variable available in every module by using `ProvidePlugin`. 
  - ```javascript
  plugins: [
    new webpack.ProvidePlugin({
      $: "jquery",
      jQuery: "jquery",
      "window.jQuery": "jquery"
    })
  ]
  ```

## demo14 exposing global variables
  - use some global variables

## demo15 hot module replacement
  - enable through webpack-dev-server: `webpack-dev-server --hot--inline`. `--hot` adds the HotModuleReplacementPlugin and switch the server to hot mode, `--inline` embed the webpack-dev-server runtime into the bundle. 
  - enable through modify `webpack.config.js`. 

## demo16 react router
  - 