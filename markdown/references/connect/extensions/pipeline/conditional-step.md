# Conditional Step

You use a conditional step to execute the next step based on a condition. 

| Property Name  | Type  | Description  |
|---|---|---|
| `expression`  | object  | Specifies the condition which must be met to execute the step within the *then* property. Otherwise the step in the *else* property is executed.  |
| `then`  | object  | Specifies the regular step that executes when the condition is met *then* can be any step type.   |
| `else`  | object  | Specifies the regular step that executes when the condition is not met. *else* can be any step type. You can omit *else*, but in this case the output of *then* must be optional.   |

> There is no output in the conditional step. The output gets defined by the step in then or else.

## Expressions

Here are the different conditions you can use when creating a conditional step:

- all: `{"all": [other expressions, all have to result in true]}`
- any: `{"any": [other expressions, at least one has to result in true]}`
- gt, gte, lt, lte: `{"gt|gte|lt|lte":[{"type":"static|input", "name|value":"nameOfInputOrValueOfStatic"}, {otherVariable}]}`
- null, notnull, ok, notok: `{"null|notnull|ok|notok":[{"name":"nameOfInput"}]}`
- eq, ne: `{"eq|ne": [{"type":"static|input","name|value":"nameOfInputOrValueOfStatic"},{otherVariable}(,...)]}`

## Pipeline Example

```json
{
  "type": "conditional",
  "input": [
    { "key": "pageId", "id": "50" }
  ],
  "expression": {
    "ne": [
      {"type":"input", "name":"pageId"},
      {"static":"input", "value":"index"}
    ]
  },
  "then": {
    "type": "pipeline",
    "id": "renderPage",
    "input": [
      {"key":"pageId", "id":"50"},
      {"key":"query", "id":"51"},
      {"key":"params", "id":"52"}
    ],
    "output": [
      {"key":"html", "id":"1000"}
    ]
  },
  "else": {
    "type": "pipeline",
    "id": "loadPage",
    "input": [
      {"key":"path", "id":"1"}
    ],
    "output": [
      {"key":"html", "id":"1000"}
    ]
  }
}
```
