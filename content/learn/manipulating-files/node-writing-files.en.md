---
title: writing-files-with-nodejs
displayTitle: 'Writing files with Node.js'
description: 'How to write files using Node.js'
authors: flaviocopes, MylesBorins, fhemberger, LaRuaNa, ahmadawais, clean99, ovflowd
category: learn
---

## Wiriting a file

The easiest way to write to files in Node.js is to use the `fs.writeFile()` API.

```js
const fs = require('fs');

const content = 'Some content!';

fs.writeFile('/Users/joe/test.txt', content, err => {
  if (err) {
    console.error(err);
  }
  // file written successfully
});
```

### Writing a file synchronously

Alternatively, you can use the synchronous version `fs.writeFileSync()`:

```js
const fs = require('fs');

const content = 'Some content!';

try {
  fs.writeFileSync('/Users/joe/test.txt', content);
  // file written successfully
} catch (err) {
  console.error(err);
}
```

You can also use the promise-based `fsPromises.writeFile()` method offered by the `fs/promises` module:

```js
const fs = require('fs/promises');

async function example() {
  try {
    const content = 'Some content!';
    await fs.writeFile('/Users/joe/test.txt', content);
  } catch (err) {
    console.log(err);
  }
}
example();
```

By default, this API will **replace the contents of the file** if it does already exist.

**You can modify the default by specifying a flag:**

```js
fs.writeFile('/Users/joe/test.txt', content, { flag: 'a+' }, err => {});
```

#### The flags you'll likely use are

* `r+` open the file for reading and writing
* `w+` open the file for reading and writing, positioning the stream at the beginning of the file. The file is created if it does not exist
* `a` open the file for writing, positioning the stream at the end of the file. The file is created if it does not exist
* `a+` open the file for reading and writing, positioning the stream at the end of the file. The file is created if it does not exist

(you can find more flags at [https://nodejs.org/api/fs.html#fs_file_system_flags](https://nodejs.org/api/fs.html#fs_file_system_flags))

## Appending content to a file

Appending to files is handy when you don't want to overwrite a filewith new content, but rather add to it.

### Examples

A handy method to append content to the end of a file is `fs.appendFile()` (and its `fs.appendFileSync()` counterpart):

```js
const fs = require('fs');

const content = 'Some content!';

fs.appendFile('file.log', content, err => {
  if (err) {
    console.error(err);
  }
  // done!
});
```

#### Example with Promises

Here is a `fsPromises.appendFile()` example:

```js
const fs = require('fs/promises');

async function example() {
  try {
    const content = 'Some content!';
    await fs.appendFile('/Users/joe/test.txt', content);
  } catch (err) {
    console.log(err);
  }
}
example();
```
