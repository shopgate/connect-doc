# Step Function

Here are the function signatures you can use to implement a step function:

- with callbacks: 
```javascript
function (context, input, cb) {
  ...
  cb(err, output) 
}
```

- with promises:
```javascript
function (context, input) {
  return new Promise ((resolve, reject) => {
    ... 
    resolve(output) || reject(err) 
  })
}
```

- with async/await: 
```javascript
async function (context, input) {
  ... 
  return output || throw err
}
```

## Context

The context contains of the following properties:
- [Logger](logger.md)
- [Storage](storage.md)
- [DeviceInfo](device-info.md)
- [AppInfo](app-info.md)
- [Meta](meta.md)
