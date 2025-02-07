# Pipeline Step

You can call a pipeline within a pipeline. For example, you might want to exclude reusable step sequences in another pipeline. Input and output of this step is equivalent to the pipeline the step calls.

## Custom properties

| Property Name   | Type  | Description  |
|---|---|---|
| `id`  | string  | Specifies the pipeline to be called |
| `trusted`  | boolean  | Specifies wether the to be called pipeline is trusted |

## Pipeline Example

```json
{
  "type": "pipeline",
  "id": "shopgate.catalog.getProducts.v1",
  "input": [
    {"key": "productId", "id": "1"}
  ],
  "output": [
    {"key": "product", "id": "10"}
  ]
}
```
