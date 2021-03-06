# s3-stream-download

  [![shippable Build][shippable-image]][shippable-url]
  [![NPM Version][npm-image]][npm-url]
  [![NPM Downloads][downloads-image]][downloads-url]

Multipart streaming download from S3

## Features

## Installation

``` bash
  $ npm install s3-stream-download --save
```

## Usage

```js
var AWS = require('aws-sdk');
var S3StreamDownload = require('./index');
var fs = require('fs');

var s3 = new AWS.S3();

var s3StreamDownload = new S3StreamDownload(s3, {Bucket: '<BUCKET>', Key:'<KEY>'});

s3StreamDownload.pipe(fs.createWriteStream('<FILENAME>'));

s3StreamDownload.on('end', function() {
    process.exit(0);
});
```

## Documentation

### new S3StreamDownload(s3, s3Params, options)

Creates a new instance of a multipart download stream.  This is a readable stream that can be
piped into other streams.

__Arguments__

* `s3` - Configured aws-sdk s3 instance.  Should be preconfigured with any credentials.
* `s3Params` - Params object that would normally be passed to s3.getObject()
* `options` - Options
    - `downloadChunkSize` - Size of each chunk in bytes.  Defaults to 5MB.
    - `concurrentChunks` - Number of chunks to download concurrently. Defaults to 5.
    - `retries` - How many times a failed chunk should be retried before failing the entire download. Retries will exponentially backoff to allow for recovery.  Defaults to 5.



## People

The author is [Chris Kinsman](https://github.com/chriskinsman) from [PushSpring](http://www.pushspring.com)

## License

  [MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/s3-stream-download.svg?style=flat
[npm-url]: https://npmjs.org/package/s3-stream-download
[downloads-image]: https://img.shields.io/npm/dm/s3-stream-download.svg?style=flat
[downloads-url]: https://npmjs.org/package/s3-stream-download
[shippable-image]: https://api.shippable.com/projects/57bfbd4c016a370e00eb8907/badge?branch=master
[shippable-url]: https://app.shippable.com/projects/57bfbd4c016a370e00eb8907
