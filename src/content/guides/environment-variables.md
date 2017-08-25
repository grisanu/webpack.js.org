---
title: Environment Variables
sort: 16
contributors:
  - simon04
  - grisanu
related:
  - title: The Fine Art of the Webpack 3 Config
    url: https://blog.flennik.com/the-fine-art-of-the-webpack-2-config-dc4d19d7f172#d60a
---

To disambiguate in your `webpack.config.js` between [development](/guides/development) and [production builds](/guides/production), you may use environment variables.

The webpack command line option `--env` allows you to pass in as many environment variables as you like, such as `--env.production` or `--env.NODE_ENV=local`. (`NODE_ENV` is commonly used as de-facto standard. See [here](https://dzone.com/articles/what-you-should-know-about-node-env)). These variables will be made accesible in the webpack config.

```
>> webpack --env.NODE_ENV=local --env.production --progress
```

There is, however a change that you will have to make to your webpack config. Typically, in your webpack config `module.exports` points to the configuration object. To use the `env` variable, you must change `module.exports` to be a function:

**webpack.config.js**

```diff
- module.exports = {
- 	entry: './src/index.js',
- 	output: {
- 		filename: 'bundle.js',
- 		path: path.resolve(__dirname, 'dist')
- 	}
- }
+ module.exports = (env) => {
+ 	/** 
+    * Use env.<YOUR VARIABLE> here:
+    *
+    * console.log(env.NODE_ENV) // 'local'
+    * console.log(env.production) // true
+    */
+    
+ 	return {
+  		entry: './src/index.js',
+  	 	output: {
+  	  		filename: 'bundle.js',
+  	  	 	path: path.resolve(__dirname, 'dist')
+  	  	}
+ 	}
+ }
```

**NOTE:** Setting up your `env` varialbe without assignment, `--env.prduction` sets `env.prduction` to `true` by default.
