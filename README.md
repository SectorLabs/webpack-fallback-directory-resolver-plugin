# webpack-fallback-directory-resolver-plugin

Fork of [kije/webpack-fallback-directory-resolver-plugin](https://github.com/kije/webpack-fallback-directory-resolver-plugin). Webpack resolver plugin to resolve modules and files through a fallback directory chain at compile time.

## Changes from upstream

* Correct `Object.assign` usage for copying default options
* Add support for Webpack v5

## Install

```
npm install @sector-labs/webpack-fallback-directory-resolver-plugin
```

## Usage

Add the plugin to the `resolve.plugins` array in your `webpack.config.js`:

```js
const FallbackDirectoryResolverPlugin = require('@sector-labs/webpack-fallback-directory-resolver-plugin');
const path = require('path');

module.exports = {
    resolve: {
        plugins: [
            new FallbackDirectoryResolverPlugin({
                prefix: 'fallback',
                directories: [
                    path.resolve(__dirname, 'js/dir2'),
                    path.resolve(__dirname, 'js/dir1')
                ]
            })
        ]
    }
};
```

Import paths use the `#<prefix>#/` format:

```js
import something from "#fallback#/my-module";
```

### Options

| Option | Default | Description |
|--------|---------|-------------|
| `prefix` | `"fallback"` | Prefix used in import paths (`#<prefix>#/...`) |
| `directories` | `[]` | Array of directory paths to search in order |
| `extensions` | `[]` | File extensions to resolve automatically (e.g. `['.js', '.jsx']`) |
| `getRegex` | `` (prefix) => `^#${prefix}#/` `` | Custom function to generate the matching regex |

## License

MIT
