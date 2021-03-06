# [gulp](https://github.com/wearefractal/gulp)-asset-manifest

> gulp plugin for adding generated assets to a manifest file

We needed to make hashed asset filenames available in a common format that a webserver (Django) could load into the templates.
This plugin can easily be modified to suit your own purposes.

It works great with [gulp-rev](https://github.com/sindresorhus/gulp-rev) by Sindre Sorhus.
`gulp-rev` adds hashes to the filename, `gulp-asset-manifest` adds the hashed filenames to the manifest.

## How it works

The plugin takes generated or processed asset files (CSS, JS, whatever) and adds them to a JSON manifest file.
It separates the files by bundles, so you can have one for CSS, one for JS and your other needs.
These bundles can then be read from the manifest file into your templates.

## Install

Install with npm

```bash
npm install gulp-asset-manifest
```

See examples below on how to add it to your gulpfile.


## Example

```js
var gulp = require('gulp');
var assetManifest = require('gulp-asset-manifest');

// Simple usage
gulp.task('default', function () {
	gulp.src('src/*.js')
		.pipe(assetManifest({bundleName: 'app_scripts'}))
		.pipe(gulp.dest('dist'));
});


// Usage with options
gulp.task('default', function () {
	gulp.src('src/*.js')
		.pipe(assetManifest({ bundleName: 'app_scripts', pathPrepend: 'build/', manifestFile: 'assets/asset_manifest.json', log: true}))
		.pipe(gulp.dest('dist'));
});


// Default usage (with gulp-rev)
var rev = require('gulp-rev'); // Optional

gulp.task('default', function () {
	gulp.src('src/*.js')
		.pipe(rev()) // Optional
		.pipe(assetManifest({bundleName: 'app_scripts', log: true}))
		.pipe(gulp.dest('dist'));
});
```

## API

### assetManifest(options)

#### options.bundleName
Type: `String`
Required: Yes

Name of the bundle for this task. 
E.g. if the tasks handles JS libraries, the bundle name could be 'js_libs'.
If the gulp task processes all Sass files, it could be 'main_css'.

#### options.manifestFile
Type: `String`
Default: `asset_manifest.json`
Required: No

Path of the manifest file which plugin reads from and writes to.

#### options.pathPrepend
Type: `String`
Default: ``
Required: No

Prepend a path to the filename. Eg. 'assets/build/'.

#### options.includeRelativePath
Type: `Boolean`
Default: `false`
Required: No

Will include the relative path of the file(s).

#### options.log
Type: `Boolean`
Default: `false`
Required: No

If true, the plugin will output filenames to the console.

## License
MIT © Vanja Cosic
