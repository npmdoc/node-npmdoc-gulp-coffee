# api documentation for  [gulp-coffee (v2.3.4)](http://github.com/contra/gulp-coffee)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-coffee.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-coffee) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-coffee.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-coffee)
#### Compile CoffeeScript files

[![NPM](https://nodei.co/npm/gulp-coffee.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-coffee)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-coffee/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-coffee/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-coffee/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-coffee/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Contra",
        "url": "http://contra.io/"
    },
    "bugs": {
        "url": "https://github.com/contra/gulp-coffee/issues"
    },
    "dependencies": {
        "coffee-script": "^1.10.0",
        "gulp-util": "^3.0.2",
        "merge": "^1.2.0",
        "through2": "^2.0.1",
        "vinyl-sourcemaps-apply": "^0.2.1"
    },
    "description": "Compile CoffeeScript files",
    "devDependencies": {
        "gulp-sourcemaps": "^2.2.0",
        "mocha": "^3.0.0",
        "should": "^11.0.0"
    },
    "directories": {},
    "dist": {
        "shasum": "e9975faf3f26746fb2e72da9e3f32c9db5746daa",
        "tarball": "https://registry.npmjs.org/gulp-coffee/-/gulp-coffee-2.3.4.tgz"
    },
    "engines": {
        "node": ">= 0.9.0"
    },
    "gitHead": "39ad603ed985b174cee687efb65cbe4f54aa571e",
    "homepage": "http://github.com/contra/gulp-coffee",
    "keywords": [
        "gulpplugin"
    ],
    "license": "MIT",
    "main": "./index.js",
    "maintainers": [
        {
            "name": "contra"
        },
        {
            "name": "fractal"
        }
    ],
    "name": "gulp-coffee",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/contra/gulp-coffee.git"
    },
    "scripts": {
        "test": "mocha"
    },
    "version": "2.3.4"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-coffee](#apidoc.module.gulp-coffee)
1.  [function <span class="apidocSignatureSpan"></span>gulp-coffee (opt)](#apidoc.element.gulp-coffee.gulp-coffee)
1.  [function <span class="apidocSignatureSpan">gulp-coffee.</span>toString ()](#apidoc.element.gulp-coffee.toString)



# <a name="apidoc.module.gulp-coffee"></a>[module gulp-coffee](#apidoc.module.gulp-coffee)

#### <a name="apidoc.element.gulp-coffee.gulp-coffee"></a>[function <span class="apidocSignatureSpan"></span>gulp-coffee (opt)](#apidoc.element.gulp-coffee.gulp-coffee)
- description and source-code
```javascript
gulp-coffee = function (opt) {
  function replaceExtension(path) {
    path = path.replace(/\.coffee\.md$/, '.litcoffee');
    return gutil.replaceExtension(path, '.js');
  }

  function transform(file, enc, cb) {
    if (file.isNull()) return cb(null, file);
    if (file.isStream()) return cb(new PluginError('gulp-coffee', 'Streaming not supported'));

    var data;
    var str = file.contents.toString('utf8');
    var dest = replaceExtension(file.path);

    var options = merge({
      bare: false,
      coffee: require('coffee-script'),
      header: false,
      sourceMap: !!file.sourceMap,
      sourceRoot: false,
      literate: /\.(litcoffee|coffee\.md)$/.test(file.path),
      filename: file.path,
      sourceFiles: [file.relative],
      generatedFile: replaceExtension(file.relative)
    }, opt);

    try {
      data = options.coffee.compile(str, options);
    } catch (err) {
      return cb(new PluginError('gulp-coffee', err));
    }

    if (data && data.v3SourceMap && file.sourceMap) {
      applySourceMap(file, data.v3SourceMap);
      file.contents = new Buffer(data.js);
    } else {
      file.contents = new Buffer(data);
    }

    file.path = dest;
    cb(null, file);
  }

  return through.obj(transform);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-coffee.toString"></a>[function <span class="apidocSignatureSpan">gulp-coffee.</span>toString ()](#apidoc.element.gulp-coffee.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
...
  }

  function transform(file, enc, cb) {
if (file.isNull()) return cb(null, file);
if (file.isStream()) return cb(new PluginError('gulp-coffee', 'Streaming not supported'));

var data;
var str = file.contents.toString('utf8');
var dest = replaceExtension(file.path);

var options = merge({
  bare: false,
  coffee: require('coffee-script'),
  header: false,
  sourceMap: !!file.sourceMap,
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
