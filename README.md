# ttag-webpack-plugin (experimental)

> This plugin is an experimental feature, if something goes wrong, still you can use `babel-plugin-ttag` to setup your localization workflow. Follow the doc - https://ttag.js.org/blog/2018/09/05/hardcore-webpack-setup.html

- `ttag` library - https://ttag.js.org/
- `ttag` and `ttag-webpack-plugin` integration - https://ttag.js.org/docs/webpack.html

Add this plugin to generate localized build for each locale. This plugin will apply `babel-ttag-plugin` with appropriate settings for each locale

> Works with Webpack4 and Babel7

## Installation

```
npm i -D ttag-webpack-plugin babel-plugin-ttag
```

### Basic usage

```js
new TtagPlugin({
  translations: {
    uk: path.join(__dirname, "./i18n/uk.po")
  }
});
```

## Options

```js
new TtagPlugin({
  translations: {
   <locale>: <path to the .po file>
  },
  filename: '[name].[locale].js',
  chunkFilename: '[id].[locale].js',
  excludedPlugins: [...],
  ttag: <babel-ttag-plugin opts>,
});
```

1. `translations`: Map of po files for locales
2. `filename` (optional): Output name of localized bundles. (default: '[name]-[locale].js')
3. `chunkFilename` (optional): Output name of localized chunks. (default: '[id].[name]-[locale].js')
4. `excludedPlugins` (optional): List of plugins you want to exclude from generating localized bundles.
5. `ttag` (optional): Possibility to pass some additional opts to `ttag-webpack-plugin`. See all available opts [here](https://ttag.js.org/docs/plugin-api.html)

## Without this plugin

A usual output from webpack output looks like this:

![Simple output](etc/without-plugin.png)

## With this plugin

With this plugin added, you will be generating localized outputs:

![Localized output](etc/with-plugin.png)

## Example:

```js
const path = require("path");
const TtagPlugin = require("ttag-webpack-plugin");

module.exports = {
  entry: {
    main: "./src/index.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: "babel-loader"
      }
    ]
  },
  plugins: [
    new TtagPlugin({
      translations: {
        uk: path.join(__dirname, "./i18n/uk.po")
      }
    })
  ]
};
```

See example - https://github.com/ttag-org/ttag-webpack-plugin/tree/master/tests-integration/fixtures/example
