# Extension Step

An extension step is the default step provided by an extension. Extension steps use a function to generate the output depending on the input.

## Custom Properties of the Extension Step

| Property Name | Type | Description |
|---|---|---|
| `id` | string | Specifies the id of the extension the step belongs to |
| `path` | string | Specifies the path to the step file. **Note**: the path property is not the exact path to the step file. For example, when the step file is located at: *project/extensions/extensionA/extension/someDir/step.js* the correct path would be: *extensionA/someDir/step.js*|

## Pipeline Example
The following example shows a general reference of an extension step and an implemented example.

```json
{
  "type": "extension", 
  "id": "<extensionId>",
  "path": "<extensionId>/<path to step relative to the "extension" folder)>",
  "input": [...],
  "output": [...]
}
```

Example:
```json
{
  "type": "extension", 
  "id": "@shopgate/catalog",
  "path": "@shopgate/catalog/getProduct.js",
  "input": [{"key": "productId", "id": "1"}],
  "output": [{"key": "product", "id": "10"}]
}
```
