# api documentation for  [html-pdf (v2.1.0)](https://github.com/marcbachmann/node-html-pdf)  [![npm package](https://img.shields.io/npm/v/npmdoc-html-pdf.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-html-pdf) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-html-pdf.svg)](https://travis-ci.org/npmdoc/node-npmdoc-html-pdf)
#### HTML to PDF converter that uses phantomjs

[![NPM](https://nodei.co/npm/html-pdf.png?downloads=true)](https://www.npmjs.com/package/html-pdf)

[![apidoc](https://npmdoc.github.io/node-npmdoc-html-pdf/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-html-pdf_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-html-pdf/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-html-pdf/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Marc Bachmann"
    },
    "bin": {
        "html-pdf": "bin/index.js"
    },
    "bugs": {
        "url": "https://github.com/marcbachmann/node-html-pdf/issues"
    },
    "dependencies": {
        "phantomjs-prebuilt": "^2.1.4"
    },
    "description": "HTML to PDF converter that uses phantomjs",
    "devDependencies": {
        "coffee-script": "^1.7.1",
        "standard": "^5.1.1",
        "tap-spec": "^2.2.0",
        "tape": "^3.4.0"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "c34d518f7f802ffbc834bf80279cfce7da2cce4b",
        "tarball": "https://registry.npmjs.org/html-pdf/-/html-pdf-2.1.0.tgz"
    },
    "engines": {
        "node": ">=4.0.0"
    },
    "gitHead": "d7ae2439ef8082475a80f3045ddfa6dce7c5054e",
    "homepage": "https://github.com/marcbachmann/node-html-pdf",
    "keywords": [
        "html",
        "pdf",
        "phantom",
        "phantomjs",
        "nodejs"
    ],
    "license": "MIT",
    "main": "lib/index.js",
    "maintainers": [
        {
            "name": "marcbachmann",
            "email": "marc.brookman@gmail.com"
        }
    ],
    "name": "html-pdf",
    "optionalDependencies": {
        "phantomjs-prebuilt": "^2.1.4"
    },
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/marcbachmann/node-html-pdf.git"
    },
    "scripts": {
        "standard": "standard bin/index.js",
        "test": "npm run standard && node test/index.js"
    },
    "version": "2.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module html-pdf](#apidoc.module.html-pdf)
1.  [function <span class="apidocSignatureSpan">html-pdf.</span>create (html, options, callback)](#apidoc.element.html-pdf.create)
1.  [function <span class="apidocSignatureSpan">html-pdf.</span>pdf (html, options)](#apidoc.element.html-pdf.pdf)
1.  object <span class="apidocSignatureSpan">html-pdf.</span>pdf.prototype

#### [module html-pdf.pdf](#apidoc.module.html-pdf.pdf)
1.  [function <span class="apidocSignatureSpan">html-pdf.</span>pdf (html, options)](#apidoc.element.html-pdf.pdf.pdf)

#### [module html-pdf.pdf.prototype](#apidoc.module.html-pdf.pdf.prototype)
1.  [function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>exec (callback)](#apidoc.element.html-pdf.pdf.prototype.exec)
1.  [function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toBuffer (callback)](#apidoc.element.html-pdf.pdf.prototype.toBuffer)
1.  [function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toFile (filename, callback)](#apidoc.element.html-pdf.pdf.prototype.toFile)
1.  [function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toStream (callback)](#apidoc.element.html-pdf.pdf.prototype.toStream)



# <a name="apidoc.module.html-pdf"></a>[module html-pdf](#apidoc.module.html-pdf)

#### <a name="apidoc.element.html-pdf.create"></a>[function <span class="apidocSignatureSpan">html-pdf.</span>create (html, options, callback)](#apidoc.element.html-pdf.create)
- description and source-code
```javascript
function createPdf(html, options, callback) {
  if (arguments.length === 1) {
    return new PDF(html)
  }

  if (arguments.length === 2 && typeof options !== 'function') {
    return new PDF(html, options)
  }

  if (arguments.length === 2) {
    callback = options
    options = {}
  }

  try {
    var pdf = new PDF(html, options)
  } catch (err) {
    return callback(err)
  }

  pdf.exec(callback)
}
```
- example usage
```shell
...
## Code example
'''javascript
var fs = require('fs');
var pdf = require('html-pdf');
var html = fs.readFileSync('./test/businesscard.html', 'utf8');
var options = { format: 'Letter' };

pdf.create(html, options).toFile('./businesscard.pdf', function(err, res) {
  if (err) return console.log(err);
  console.log(res); // { filename: '/app/businesscard.pdf' }
});
'''

## API
...
```

#### <a name="apidoc.element.html-pdf.pdf"></a>[function <span class="apidocSignatureSpan">html-pdf.</span>pdf (html, options)](#apidoc.element.html-pdf.pdf)
- description and source-code
```javascript
function PDF(html, options) {
  this.html = html
  this.options = options || {}
  if (this.options.script) {
    this.script = path.normalize(this.options.script)
  } else {
    this.script = path.join(__dirname, 'scripts', 'pdf_a4_portrait.js')
  }

  if (this.options.filename) this.options.filename = path.resolve(this.options.filename)
  if (!this.options.phantomPath) this.options.phantomPath = phantomjs && phantomjs.path
  this.options.phantomArgs = this.options.phantomArgs || []
  assert(this.options.phantomPath, "html-pdf: Failed to load PhantomJS module. You have to set the path to the PhantomJS binary
using 'options.phantomPath'")
  assert(typeof this.html === 'string' && this.html.length, "html-pdf: Can't create a pdf without an html string")
  this.options.timeout = parseInt(this.options.timeout) || 30000
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.html-pdf.pdf"></a>[module html-pdf.pdf](#apidoc.module.html-pdf.pdf)

#### <a name="apidoc.element.html-pdf.pdf.pdf"></a>[function <span class="apidocSignatureSpan">html-pdf.</span>pdf (html, options)](#apidoc.element.html-pdf.pdf.pdf)
- description and source-code
```javascript
function PDF(html, options) {
  this.html = html
  this.options = options || {}
  if (this.options.script) {
    this.script = path.normalize(this.options.script)
  } else {
    this.script = path.join(__dirname, 'scripts', 'pdf_a4_portrait.js')
  }

  if (this.options.filename) this.options.filename = path.resolve(this.options.filename)
  if (!this.options.phantomPath) this.options.phantomPath = phantomjs && phantomjs.path
  this.options.phantomArgs = this.options.phantomArgs || []
  assert(this.options.phantomPath, "html-pdf: Failed to load PhantomJS module. You have to set the path to the PhantomJS binary
using 'options.phantomPath'")
  assert(typeof this.html === 'string' && this.html.length, "html-pdf: Can't create a pdf without an html string")
  this.options.timeout = parseInt(this.options.timeout) || 30000
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.html-pdf.pdf.prototype"></a>[module html-pdf.pdf.prototype](#apidoc.module.html-pdf.pdf.prototype)

#### <a name="apidoc.element.html-pdf.pdf.prototype.exec"></a>[function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>exec (callback)](#apidoc.element.html-pdf.pdf.prototype.exec)
- description and source-code
```javascript
function PdfExec(callback) {
  var callbacked = false
  var child = childprocess.spawn(this.options.phantomPath, [].concat(this.options.phantomArgs, [this.script]))
  var stdout = []
  var stderr = []
  var timeout = setTimeout(function execTimeout () {
    child.stdin.end()
    child.kill()
    if (!stderr.length) {
      stderr = [new Buffer('html-pdf: PDF generation timeout. Phantom.js script did not exit.')]
    }
  }, this.options.timeout)

  child.stdout.on('data', function (buffer) {
    return stdout.push(buffer)
  })

  child.stderr.on('data', function (buffer) {
    stderr.push(buffer)
    child.stdin.end()
    return child.kill()
  })

  function exit (err, data) {
    if (callbacked) return
    callbacked = true
    clearTimeout(timeout)
    if (err) return callback(err)
    return callback(null, data)
  }

  child.on('error', exit)

  child.on('exit', function (code) {
    if (code || stderr.length) {
      var err = new Error(Buffer.concat(stderr).toString() || 'html-pdf: Unknown Error')
      return exit(err)
    } else {
      try {
        var buff = Buffer.concat(stdout).toString()
        var data = (buff) != null ? buff.trim() : undefined
        data = JSON.parse(data)
      } catch (err) {
        return exit(err)
      }
      return exit(null, data)
    }
  })

  var res = JSON.stringify({html: this.html, options: this.options})
  return child.stdin.write(res + '\n', 'utf8')
}
```
- example usage
```shell
...
this.options.phantomArgs = this.options.phantomArgs || []
assert(this.options.phantomPath, "html-pdf: Failed to load PhantomJS module. You have to set the path to the PhantomJS binary using
 'options.phantomPath'")
assert(typeof this.html === 'string' && this.html.length, "html-pdf: Can't create a pdf without an html string")
this.options.timeout = parseInt(this.options.timeout) || 30000
}

PDF.prototype.toBuffer = function PdfToBuffer (callback) {
this.exec(function execPdfToBuffer (err, res) {
  if (err) return callback(err)
  fs.readFile(res.filename, function readCallback (err, buffer) {
    if (err) return callback(err)
    fs.unlink(res.filename, function unlinkPdfFile (err) {
      if (err) return callback(err)
      callback(null, buffer)
    })
...
```

#### <a name="apidoc.element.html-pdf.pdf.prototype.toBuffer"></a>[function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toBuffer (callback)](#apidoc.element.html-pdf.pdf.prototype.toBuffer)
- description and source-code
```javascript
function PdfToBuffer(callback) {
  this.exec(function execPdfToBuffer (err, res) {
    if (err) return callback(err)
    fs.readFile(res.filename, function readCallback (err, buffer) {
      if (err) return callback(err)
      fs.unlink(res.filename, function unlinkPdfFile (err) {
        if (err) return callback(err)
        callback(null, buffer)
      })
    })
  })
}
```
- example usage
```shell
...
  console.log(res.filename);
});

pdf.create(html).toStream(function(err, stream){
  stream.pipe(fs.createWriteStream('./foo.pdf'));
});

pdf.create(html).toBuffer(function(err, buffer){
  console.log('This is a buffer:', Buffer.isBuffer(buffer));
});


// for backwards compatibility
// alias to pdf.create(html[, options]).toBuffer(callback)
pdf.create(html [, options], function(err, buffer){});
...
```

#### <a name="apidoc.element.html-pdf.pdf.prototype.toFile"></a>[function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toFile (filename, callback)](#apidoc.element.html-pdf.pdf.prototype.toFile)
- description and source-code
```javascript
function PdfToFile(filename, callback) {
  assert(arguments.length > 0, 'html-pdf: The method .toFile([filename, ]callback) requires a callback.')
  if (filename instanceof Function) {
    callback = filename
    filename = undefined
  } else {
    this.options.filename = path.resolve(filename)
  }
  this.exec(callback)
}
```
- example usage
```shell
...
## Code example
'''javascript
var fs = require('fs');
var pdf = require('html-pdf');
var html = fs.readFileSync('./test/businesscard.html', 'utf8');
var options = { format: 'Letter' };

pdf.create(html, options).toFile('./businesscard.pdf', function(err, res) {
  if (err) return console.log(err);
  console.log(res); // { filename: '/app/businesscard.pdf' }
});
'''

## API
...
```

#### <a name="apidoc.element.html-pdf.pdf.prototype.toStream"></a>[function <span class="apidocSignatureSpan">html-pdf.pdf.prototype.</span>toStream (callback)](#apidoc.element.html-pdf.pdf.prototype.toStream)
- description and source-code
```javascript
function PdfToStream(callback) {
  this.exec(function (err, res) {
    if (err) return callback(err)
    try {
      var stream = fs.createReadStream(res.filename)
    } catch (err) {
      return callback(err)
    }

    stream.on('end', function () {
      fs.unlink(res.filename, function (err) {
        if (err) console.log('html-pdf:', err)
      })
    })

    callback(null, stream)
  })
}
```
- example usage
```shell
...

'''js
var pdf = require('html-pdf');
pdf.create(html).toFile([filepath, ]function(err, res){
  console.log(res.filename);
});

pdf.create(html).toStream(function(err, stream){
  stream.pipe(fs.createWriteStream('./foo.pdf'));
});

pdf.create(html).toBuffer(function(err, buffer){
  console.log('This is a buffer:', Buffer.isBuffer(buffer));
});
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
