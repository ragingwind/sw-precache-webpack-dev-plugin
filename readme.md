# sw-precache-webpack-dev-server-plugin

> Webpack Plugin for using sw-precache during development with webpack-dev-server

![screen shot 2017-01-30 at 7 08 40 pm](https://cloud.githubusercontent.com/assets/124117/22424472/119a2b7e-e73a-11e6-8b4f-325bc0f81339.png)

## Install

```sh
$ yarn add --dev sw-precache-webpack-dev-server-plugin
```

or
```sh
$ npm install --save sw-precache-webpack-dev-server-plugin
```

### How it works

*DISCLAIMER*: This plugin isn't able to be work perfectly because of using workaround codes to support memory-fs in webpack. And when it comes to manage including ambiguous expression of path, For examples, ['*.js', '*.html'], in that case, it couldn't make a right judge for location between physical file path and memory-fs. Therefore, we recommand you use more specific glob patterns for that, like absolute path or relative path expressions.

This plugin will be applied after `all of assets has been emmited by webpack compiling`. It means that all of files you wanted to cached by service worker will be listed in assets after webpack compiler. To achive that, you need to use webpack plugins(Copy or ...) to register it, then sw.js will be wrote in temporory on memory-fs. webpack dev server will serve sw.js file. Recently, [the version supports glob patterns for files located in physical path](https://github.com/ragingwind/sw-precache-webpack-dev-server-plugin/commit/8babdf7938609f6db5178859b88f6f3365e285c6#diff-168726dbe96b3ce427e7fedce31bb0bcR23) not on memory-fs of webpack. Although, uing webpack plugins is a still recommendation that to make server worker will be working well.

## Usage

See [basic webpack config files](./example/webpack.config.js) at examples.

### How to test

You can test this plugin by running example application with below commands. It will manage a service worker script while webpack devserver is running. Warn you, you need to make sure that the previous service worker script must be ungresitered or refleshed before you test with a newer version script of updating service worker configuration at webpack config.

```sh
$ yarn start
```

or
```sh
$ npm start
```

and open browser, visit to `localhost:8080`

## Configuration

It will accept and pass through all of [options parameter of sw-precache](https://github.com/GoogleChrome/sw-precache#options-parameter) to [sw-precache](https://github.com/GoogleChrome/sw-precache). By the way, there are more options and a few of specical way to treats passed configurations.

### sw-precache Configurations

- staticFileGlobs: [Array<String>] - Default is empty array, allow dev server to cache all of files in assets on webpack complilation

### Plugin Configurations

- filename: [String] - Service worker script name for serving on dev server. It is same with [sw-precache-webpack-plugin](https://github.com/goldhand/sw-precache-webpack-plugin#configuration).

## Test

It will be covered soon

## License

MIT © [Jimmy Moon](http://ragingwind.me)
