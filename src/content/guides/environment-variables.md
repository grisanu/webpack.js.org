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

To disambiguate between [development](/guides/development) and [production](/guides/production) builds in your `webpack.config.js`, you may want to use environment variables.

The webpack command line [environment option](/api/cli/#environment-options), `--env` allows you to pass in as many environment variables as you would like. Environment variables will be made accesible in your `webpack.config.js`. For example, `--env.production` or `--env.NODE_ENV=local` (`NODE_ENV` is conventionally used to define the environment type, see [here](https://dzone.com/articles/what-you-should-know-about-node-env).)

```
>> webpack --env.NODE_ENV=local --env.production --progress
```

T> Setting up your `env` variable without assignment, `--env.prduction` sets `env.prduction` to `true` by default. See the [webpack CLI](/api/cli/#environment-options) documentation for more information.

Howeve, there is a change that you will have to make to your `webpack.config.js`. Typically, in your webpack configuration file `module.exports` points to the configuration object. To use the `env` variable, you must change `module.exports` to be a function:

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
