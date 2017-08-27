# Webpack Workflow

## Basic
1. install ```npm```
2. install packages
	
	```
	$ npm i 
		webpack 
		webpack-dev-server
		webpack-merge 
		css-loader 
		style-loader 
		file-loader 
		url-loader 
		babel-loader 
		babel-core 
		babel-plugin-transform-runtime 
		babel-preset-es2015 
		vue-loader 
		vue-hot-reload-api
		vue-template-compiler 
		-D
	```
3. add ```webpack.config.js```

	```
	var path = require('path');
	var webpack = require('webpack');
	
	var entry = {
	  main: path.join(__dirname, 'src', 'main'),
	};
	
	var config = {
	  entry,
	  plugins: [
	    new webpack.HotModuleReplacementPlugin()
	  ],
	  output: {
	    path: path.join(__dirname, 'dist'),
	    filename: 'bundle.js',
	    publicPath: '/dist/'
	  },
	  module: {
	    rules: [
	      {
	        test: /\.js$/,
	        loader: "babel-loader", // Do not use "use" here
	        exclude: /node_modules/
	      },
	      {
	        test: /\.vue$/,
	        loader: 'vue-loader'
	      }
	    ]
	  },
	  resolve: {
	    extensions: ['.js', '.vue'],
	    /**
	     * Vue v2.x 之後 NPM Package 預設只會匯出 runtime-only 版本，若要使用 standalone 功能則需下列設定
	     */
	    alias: {
	      vue: 'vue/dist/vue.js'
	    }
	  }
	}
	
	module.exports = config
	```
4. add `.babelrc`
	
	```
	{
	  "presets": ["es2015"],
	  "plugins": ["transform-runtime"]
	}
	```
5. add `main.vue`
	
	```
	import Vue from 'vue'
	import App from './app.vue'
	
	new Vue({
	  el: '#app',
	  components: { App }
	})
	```

6. add `app.vue`

	```
	<template lang="html">
	  <div>
	    <div class="message">
	      {{ message }}
	    </div>
	  </div>
	</template>
	
	<script>
	export default {
	  data () {
	    return {
	      message: 'Helo, Vue.js 2.0'
	    }
	  }
	}
	</script>
	
	<style lang="css">
	.message {
	  color: pink;
	  font-size: 1.4em;
	}
	</style>
	```

### Note
```
注意 require 的 path 分成 函式庫 相對路徑 絕對路徑

函式庫：什麼都不加，單純 library name
相對路徑：./ 開頭
絕對路徑：/ 開頭
```

## Webpack workflow with Yii

> author: KettanWu
> 
> reop: [git](https://github.com/iamken1204/webpack.workflow.backend)

1. Install 

	* [nvm](https://github.com/creationix/nvm#install-script) - Node Version Manager
	
	- The script clones the nvm repository to ~/.nvm and adds the source line to your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).
	
	```
		export NVM_DIR="$HOME/.nvm"
		[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
	```	
	
	- Reload bash sources	
	
	***
	
	* ```nvm install node```
	
	* Check versions ```nvm use node```, ```npm|node -v```

2. Webpack Structure

	#### /webpack.config.js

	* **output.path**: root output path
	
	```
	module.exports = {
	  entry,
	  // Kettan:
	  // [name] correspond to config.entry's key
	  output: {
	    path: path.resolve(__dirname, './public/dist'),
	    publicPath: '/dist/',
	    filename: '[name].js',
	    libraryTarget: 'umd'
	  },
	}
	```
	
	* **base asset:** /assets/assets.js
