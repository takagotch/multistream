### multistream
---
https://github.com/feross/multistream

```
npm install multistream
```

```js
var MultiStream = require('multistream')
var fs = require('fs')

var stream = [
  fs.createReadStream(__dirname + '/numbers/1.txt'),
  fs.createReadStream(__dirname + '/numbers/2.txt'),
  fs.createReadStream(__dirname + '/numbers/3.txt')
]
new MultiStream(stream).pipe(process.stdout)

var streams = [
  fs.createReadStream(__dirname + '/numbers/1.txt'),
  function(){
    return fs.createReadStream(__dirname + '/numbers/2.txt')
  },
  function(){
    return fs.createReadStream(__dirname + '/numbers/3.txt')
  }
]
new MultiStream(streams).pipe(process.stdout)

var count = 0;
function factory (cb){
  if(count > 3) return cb(null, null)
  count++
  setTimeout(function(){
    cb(null, fs.createReadStream(__dirname + '/numbers/' + count + '.txt'))
  }, 100)
}
new MultiStream(factory).pipe(process.stdout)

```

```
```


