## About

[Request](https://github.com/mikeal/request) is a great HTTP client for NodeJS,
but if you deal only with JSON, things could be more straightforward. This lib
aims to simplify Request usage for JSON only requests. The API is simpler and
it comes with very few dependencies.

If you want a more featured version of this lib, have a look at 
[request-json](https://github.com/cozy/request-json) which is based on request
and that way provides as many features (but with more dependencies!).

## Install

Add it to your package.json file or run in your project folder:

    npm install request-json-light

## How it works

```javascript
request = require('request-json-light');
var client = request.newClient('http://localhost:8888/');

var data = {
  title: 'my title',
  content: 'my content'
};
client.post('posts/', data, function(err, res, body) {
  return console.log(res.statusCode);
});

client.get('posts/', function(err, res, body) {
  return console.log(body.rows[0].title);
});

data = {
  title: 'my new title'
};
client.put('posts/123/', data, function(err, res, body) {
  return console.log(response.statusCode);
});

client.del('posts/123/', function(err, res, body) {
  return console.log(response.statusCode);
});

data = {
  title: 'my patched title'
};
client.patch('posts/123/', data, function(err, res, body) {
  return console.log(response.statusCode);
});
```

### Extra : files

```javascript
data = {
  name: "test"
};
client.sendFile('attachments/', './test.png', data, function(err, res, body) {
  if (err) {
    return console.log(err);
  }
});

client.saveFile('attachments/test.png', './test-get.png', function(err, res, body) {
  if (err) {
    return console.log(err);
  }
});

```

`sendFile` can support file path, stream, array of file path and array of
streams. Each file is stored with the key 'file + index' (file0, file1,
file2...) in the request in case of array. For a single value, it is stored in
the field with key 'file'.
If you use a stream, it must have a "path" attribute containing its path or filename.


### Extra : basic authentication

```javascript
client.setBasicAuth('john', 'secret');
client.get('private/posts/', function(err, res, body) {
  return console.log(body.rows[0].title);
});

```
