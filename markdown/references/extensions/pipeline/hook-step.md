# Hook Step
A hook step is a named placeholder where an extension can insert specified steps automatically. 

## Custom Properties of the Hook Step

| Property Name | Type | Description |
| --- | --- | --- |
| `id` | string | Specifies the ID of the hook point. Use this id as the reference for the `step.hooks` property within the extension configuration of the step providing extension. |

## Pipeline Example

The following example shows a general reference of a hook step and an implemented example.

General Step Reference:

```json
{
  "type": "hook",
  "id": "<hookId>",
  "input": [...],
  "output": [...]
}
```

Implemented example:

```json
{
  "type": "hook",
  "id": "getProductImageUrl",
  "input": [{"key": "productId", "id": "1"}],
  "output": [{"key": "imageUrl", "id": "10"}]
}
```

## Default Hooks

By default, `before` and `after` hook steps are available in all pipelines. The steps inserted in the `before` hook can consume and manipulate all inputs of the pipeline. The steps inserted in the `after` hook can consume and manipulate all inputs and outputs of the pipeline.

> **Note:** Creating custom hook steps named `before` or `after` within a pipeline file will result in an error.

## Extension Configuration

The extension-config.json supports a specific key called `steps`. The extension developer can define in this key which steps are included in this extension and which should be exposed. Furthermore, the developer can define in which hook this step should be included. One step can be included in multiple hooks.

Example:
```
{
  "version": "1.0.0",
  "id": "@shopgate/awesomeHooks",
  "components": [],
  "steps": [
    {
      "path": "extension/myAwesomeStep.js",
      "description": "This step must be placed before any other steps because of all the awesome things it does.",
      "hooks" : ["shopgate.catalog.getProducts.v1:after", "*:before"],
      "input" : [
        {"key": "categoryId"}
      ],
      "output" : [
        {"key": "categoryId"}
      ]
    }
  ]
}
```
All objects in the "steps" need to follow this schema:

| Field | Description | Possible Value |
| --- | --- | --- |
| Path | Path to the extension step, including the "extension" folder. **Note**: Steps outside the extension will throw an error. | extension/{stepfile} |
 Description (optional) | A short description of what the step does and what a system integrator needs to know to properly place it in the pipeline(s). | Adds field 'payment_information'; should be placed before any payment processing steps. |
 Hooks (optional) | Target where the step should be pushed in. It is a list of hook strings. **Note**: This field is not required. If the step should not be pushed into a hook, remove it.| See "Hook String" |
  Input | Input of the step. If the step is made for a hook, the names need to match the input's name of the hooks.| See "Dynamic Input And Output" |
  Output | Output of the step. Within the step, align property names of your returned object to match those defined here. | See "Dynamic Input And Output" |

  ## Hook String

A hook string consists of the pipeline name and a hook name, separated by a colon. The hooks are defined in the `target` key on every step. If the step should not be included in a hook, the array can be empty or the target can be removed.
```
{pipelineName}:{hookName}
```
To have a step included in all hooks of a certain name, regardless of the pipeline, use the asterisk wildcard as pipeline name:
```
*:{hookName}
```
**Note:** Steps are only included in hooks of pipelines with the same trust level (trusted/untrusted). 

| Field | Description | Possible Value |
| --- | --- | --- |
| pipelineName | The pipeline that has the hook into which the step should be injected or the asterisk character to include the step into every pipeline that has a hook of the specified name. | any pipeline name or *|
 Target | Every hook in a pipeline has a unique identifier. The hooks "before" and "after" are pre-defined and automatically available for every pipeline. Those are therefore reserved. | beforeSomeAction, afterSomeAction |

 ## Dynamic Input and Output

 You might need to work with additional input values or add additional keys to the output.

 ### Input 

 In order to add additional input values, you must define them as objects in the "inputs" array:
 ```
 {
  "key": "someInput",
  "optional": true,
  "addPipelineInput": true
}
```
| Field | Description | Possible Value |
| --- | --- | --- |
| Optional | Defines if the input is required (false) or optional (true) | true, false |
 Key | The key of the input | someInput |
Internal | Defines if the input is internal | true, false |
addPipelineInput | Defines if the input should be added to the pipeline's input array | true, false |

### Output

In order to add additional output values, you must define them as objects in the "outputs" array:
```
{
  "key": "someOutput",
  "optional": true,
  "addPipelineOutput": true
}
```
| Field | Description | Possible Value |
| --- | --- | --- |
| Optional | Defines if the output is required (false) or optional (true) | true, false |
 Key | The key of the output | someOutput |
Internal | Defines if the output is internal | true, false |
addPipelineOutput | Defines if the output should be added to the pipeline's output array | true, false |
