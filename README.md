# Rollup multiple .scss, .sass and .css imports

WARNING: This is a fork with some changes required for personal needs.

New features includes:
- remove `node-sass` from dependencies, auto-recognize `sass` library from installed modules
- generate source map for build

If my PR will be merged or similar functionality will be implemented in original project, this project will be deleted without notice.


<a href="LICENSE">
  <img src="https://img.shields.io/badge/license-MIT-brightgreen.svg" alt="Software License" />
</a>
<a href="https://github.com/astappiev/rollup-plugin-scss/issues">
  <img src="https://img.shields.io/github/issues/astappiev/rollup-plugin-scss.svg" alt="Issues" />
</a>
<a href="http://standardjs.com/">
  <img src="https://img.shields.io/badge/code%20style-standard-brightgreen.svg" alt="JavaScript Style Guide" />
</a>
<a href="https://npmjs.org/package/@astappiev/rollup-plugin-scss">
  <img src="https://img.shields.io/npm/v/@astappiev/rollup-plugin-scss.svg?style=flat-squar" alt="NPM" />
</a>
<a href="https://github.com/astappiev/rollup-plugin-scss/releases">
  <img src="https://img.shields.io/github/release/astappiev/rollup-plugin-scss.svg" alt="Latest Version" />
</a>

## Installation
```
npm install --save-dev rollup-plugin-scss
```

## Usage
```js
// rollup.config.js
import scss from 'rollup-plugin-scss'

export default {
  input: 'input.js',
  output: {
    file: 'output.js',
    format: 'esm'
  },
  plugins: [
    scss() // will output compiled styles to output.css
  ]
}
```

```js
// entry.js
import './reset.scss'
```

### Options

Options are passed to the sass compiler ([node-sass] by default). Refer to [ the Sass docs](https://sass-lang.com/documentation/js-api#options) for more details on these options. <br/>
One notable option is `indentedSyntax` which you'll need if you're parsing Sass syntax instead of Scss syntax. (e.g. when extracting a Vue `<style lang="sass">` tag) <br/>
By default the plugin will base the filename for the css on the bundle destination.

```js
scss({
  // Choose *one* of these possible "output:..." options
  // Default behaviour is to write all styles to the bundle destination where .js is replaced by .css
  output: true,

  // Filename to write all styles to
  output: 'bundle.css',

  // Callback that will be called ongenerate with two arguments:
  // - styles: the contents of all style tags combined: 'body { color: green }'
  // - styleNodes: an array of style objects: { filename: 'body { ... }' }
  output: function (styles, styleNodes) {
    writeFileSync('bundle.css', styles)
  },

  // Disable any style output or callbacks, import as string
  output: false,
  
  // Choose files to include in processing (default: ['/**/*.css', '/**/*.scss', '/**/*.sass'])
  include: [],
  
  // Choose files to exclude from processing, (default: undefined) 
  exclude: [],

  // Determine if node process should be terminated on error (default: false)
  failOnError: true,

  // Prefix global scss. Useful for variables and mixins.
  prefix: `@import "./fonts.scss";`,

  // Use a node-sass compatible compiler (default: node-sass)
  sass: require('sass'),

  // Run postcss processor before output
  processor: css => postcss([autoprefixer({ overrideBrowserslist: "Edge 18" })]),

  // Process resulting CSS
  processor: css => css.replace('/*date*/', '/* ' + new Date().toJSON() + ' */'),

  // Add file/folder to be monitored in watch mode so that changes to these files will trigger rebuilds.
  // Do not choose a directory where rollup output or dest is pointed to as this will cause an infinite loop
  watch: 'src/styles/components',
  watch: ['src/styles/components', 'src/multiple/folders'],
})
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Contributions and feedback are very welcome.

To get it running:
  1. Clone the project.
  2. `npm install`

## Credits

- [Thomas Ghysels](https://github.com/thgh)
- [All Contributors][link-contributors]

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.

[link-author]: https://github.com/thgh
[link-contributors]: ../../contributors
[rollup-plugin-vue]: https://www.npmjs.com/package/rollup-plugin-vue
[rollup-plugin-buble]: https://www.npmjs.com/package/rollup-plugin-buble
[rollup-plugin-babel]: https://www.npmjs.com/package/rollup-plugin-babel
[node-sass]: https://www.npmjs.com/package/node-sass
[sass]: https://www.npmjs.com/package/sass
