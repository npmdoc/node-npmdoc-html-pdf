# npmdoc-html-pdf

#### api documentation for  [html-pdf (v2.1.0)](https://github.com/marcbachmann/node-html-pdf)  [![npm package](https://img.shields.io/npm/v/npmdoc-html-pdf.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-html-pdf) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-html-pdf.svg)](https://travis-ci.org/npmdoc/node-npmdoc-html-pdf)

#### HTML to PDF converter that uses phantomjs

[![NPM](https://nodei.co/npm/html-pdf.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/html-pdf)

- [https://npmdoc.github.io/node-npmdoc-html-pdf/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-html-pdf/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-html-pdf/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-html-pdf/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-html-pdf/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-html-pdf/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "name": "html-pdf",
    "version": "2.1.0",
    "description": "HTML to PDF converter that uses phantomjs",
    "engines": {
        "node": ">=4.0.0"
    },
    "main": "lib/index.js",
    "directories": {
        "test": "test"
    },
    "bin": {
        "html-pdf": "bin/index.js"
    },
    "scripts": {
        "standard": "standard bin/index.js",
        "test": "npm run standard && node test/index.js"
    },
    "author": "Marc Bachmann",
    "license": "MIT",
    "devDependencies": {
        "coffee-script": "^1.7.1",
        "standard": "^5.1.1",
        "tap-spec": "^2.2.0",
        "tape": "^3.4.0"
    },
    "optionalDependencies": {
        "phantomjs-prebuilt": "^2.1.4"
    },
    "repository": {
        "type": "git",
        "url": "git://github.com/marcbachmann/node-html-pdf.git"
    },
    "keywords": [
        "html",
        "pdf",
        "phantom",
        "phantomjs",
        "nodejs"
    ],
    "bugs": {
        "url": "https://github.com/marcbachmann/node-html-pdf/issues"
    },
    "homepage": "https://github.com/marcbachmann/node-html-pdf"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
