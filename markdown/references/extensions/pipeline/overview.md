# Pipeline

A pipeline is a list of steps with a defined input and output. Pipelines can either be public or private. You can only call private pipelines by other pipelines in the same environment (trusted or regular).

Pipeline steps can have different types. [See Step reference](markdown/references/extensions/steps/overview.md).

The following example shows the basic structure of a pipeline.

```json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.testPipelines.doSth.v1",
    "public": true,
    "input": [
      { "key": "pipelineInput1", "id": "1" },
      { "key": "pipelineInput2", "id": "2", "optional": true }
    ],
    "output": [
      { "key": "pipelineOutput1", "id": "1" },
      { "key": "pipelineOutput2", "id": "10" },
      { "key": "pipelineOutput3", "id": "11", "optional": true }
    ],
    "steps": [{
      "type": "extension",
      "id": "@shopgate/testPipelines",
      "path": "@shopgate/testPipelines/someSteps/doSth.js",
      "input": [
        { "key": "input1", "id": "1" }],
      "output": [
        { "key": "output2", "id": "10" }
      ]
    }, {
      "type": "extension",
      "id": "@shopgate/crazyPipelines",
      "path": "@shopgate/crazyPipelines/greatSteps/doSthElse.js",
      "input": [
        { "key": "input2", "id": "2", "optional": true },
        { "key": "output2", "id": "10" }
      ],
      "output": [
        { "key": "output3", "id": "11", "optional": true }
      ]
    }]
  }
}
```

| Key | Type | Description |
|---|---|---|
| `version` | string | Provides the version of the pipeline configuration format |
| `pipeline` | object | Specifies properties of this specific pipeline |
| `pipeline.id` | string | Specifies the pipeline’s id which has to match the pipeline file name |
| `pipeline.public` | boolean | Indicates if the pipeline is publically available for pipeline calls |
| `pipeline.input` | array\<object> | Specifies the input schema for this pipeline |
| `pipeline.output` | array\<object> | Specifies the output schema for this pipeline |
| `pipeline.steps` | array\<object> | Provides the step objects which must execute to fully process this pipeline |
