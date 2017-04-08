# api documentation for  [wiredep (v4.0.0)](https://github.com/taptapship/wiredep#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-wiredep.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-wiredep) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-wiredep.svg)](https://travis-ci.org/npmdoc/node-npmdoc-wiredep)
#### Wire Bower dependencies to your source code.

[![NPM](https://nodei.co/npm/wiredep.png?downloads=true)](https://www.npmjs.com/package/wiredep)

[![apidoc](https://npmdoc.github.io/node-npmdoc-wiredep/build/screenCapture.buildNpmdoc.browser.%252Fhome%252Ftravis%252Fbuild%252Fnpmdoc%252Fnode-npmdoc-wiredep%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-wiredep/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-wiredep/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-wiredep/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Stephen Sawchuk",
        "email": "sawchuk@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/taptapship/wiredep/issues"
    },
    "dependencies": {
        "bower-config": "^1.3.0",
        "glob": "^7.0.3",
        "lodash": "^4.6.1",
        "propprop": "^0.3.0",
        "through2": "^2.0.1",
        "wiredep-cli": "^0.1.0"
    },
    "description": "Wire Bower dependencies to your source code.",
    "devDependencies": {
        "chai": "^3.5.0",
        "fs-extra": "^0.26.7",
        "istanbul": "^0.4.2",
        "jshint": "*",
        "mocha": "*"
    },
    "directories": {},
    "dist": {
        "shasum": "ee9548a9504dfe7e85401a435dbed2c9b4ea2e44",
        "tarball": "https://registry.npmjs.org/wiredep/-/wiredep-4.0.0.tgz"
    },
    "files": [
        "lib/",
        "LICENSE",
        "wiredep.js"
    ],
    "gitHead": "3416e1e6eb61b1498adcdf9dd42262a01fdc1b19",
    "homepage": "https://github.com/taptapship/wiredep#readme",
    "keywords": [
        "bower",
        "package",
        "management",
        "inject",
        "script",
        "dependencies"
    ],
    "license": "MIT",
    "main": "./wiredep.js",
    "maintainers": [
        {
            "name": "cwspear",
            "email": "cam@cameronspear.com"
        },
        {
            "name": "eddiemonge",
            "email": "eddie+npm@eddiemonge.com"
        },
        {
            "name": "ruyadorno",
            "email": "contact@ruyadorno.com"
        },
        {
            "name": "stephenplusplus",
            "email": "sawchuk@gmail.com"
        }
    ],
    "name": "wiredep",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/taptapship/wiredep.git"
    },
    "scripts": {
        "coverage": "istanbul cover _mocha -- -R spec",
        "test": "jshint *.js lib/*.js test/*.js && NODE_ENV=test mocha -R spec"
    },
    "version": "4.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module wiredep](#apidoc.module.wiredep)
1.  [function <span class="apidocSignatureSpan">wiredep.</span>stream (opts)](#apidoc.element.wiredep.stream)
1.  object <span class="apidocSignatureSpan">wiredep.</span>helpers

#### [module wiredep.helpers](#apidoc.module.wiredep.helpers)
1.  [function <span class="apidocSignatureSpan">wiredep.helpers.</span>createStore ()](#apidoc.element.wiredep.helpers.createStore)



# <a name="apidoc.module.wiredep"></a>[module wiredep](#apidoc.module.wiredep)

#### <a name="apidoc.element.wiredep.stream"></a>[function <span class="apidocSignatureSpan">wiredep.</span>stream (opts)](#apidoc.element.wiredep.stream)
- description and source-code
```javascript
stream = function (opts) {
  opts = opts || {};

  return $.through2.obj(function (file, enc, cb) {
    if (file.isNull()) {
      this.push(file);
      return cb();
    }

    if (file.isStream()) {
      this.emit('error', 'Streaming not supported');
      return cb();
    }

    try {
      opts.stream = {
        src: file.contents.toString(),
        path: file.path,
        fileType: $.path.extname(file.path).substr(1)
      };

      file.contents = new Buffer(wiredep(opts));
    } catch (err) {
      this.emit('error', err);
    }

    this.push(file);
    cb();
  });
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.wiredep.helpers"></a>[module wiredep.helpers](#apidoc.module.wiredep.helpers)

#### <a name="apidoc.element.wiredep.helpers.createStore"></a>[function <span class="apidocSignatureSpan">wiredep.helpers.</span>createStore ()](#apidoc.element.wiredep.helpers.createStore)
- description and source-code
```javascript
createStore = function () {
  var bucket = {};

<span class="apidocCodeCommentSpan">  /**
   * Sets a property on the store, with the given value.
   *
   * @param  {string} property  an identifier for the data
   * @param  {*}      value     the value of the data being stored
   * @return {function} the set function itself to allow chaining
   */
</span>  var set = function (property, value) {
    bucket[property] = value;
    return set;
  };

  /**
   * Returns the store item asked for, otherwise all of the items.
   *
   * @param  {string|undefined} property  the property being requested
   * @return {*} the store item that was matched
   */
  var get = function (property) {
    if (!property) {
      return bucket;
    }

    return bucket[property];
  };

  return {
    set: set,
    get: get
  };
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
