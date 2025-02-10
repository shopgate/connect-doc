# Error Catch Extension Step

Step executions within a pipeline can result in an error. You can catch errors with an *ErrorCatchExtensionStep*.

**Step function:**

```javascript
module.exports = (err, context, input) => {
  // catch err in any way if present
}
```

> The input of an error catch extension step must be optional because it could be called with an error or regular input (which won't exist if an error was passed).

## Use in pipeline

```json
{
  "type": "errorCatchExtension", 
  "id": "<extensionId>",
  "path": "<extensionId>/<path to step relative to the extensions extension folder)>",
  "input": [...],
  "output": [...]
}
```
