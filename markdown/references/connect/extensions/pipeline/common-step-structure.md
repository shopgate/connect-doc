# Step

Within a pipeline, steps are represented as a JSON object with certain properties. Here are the properties all step types share:

| Property Name	  | Type  | Description  |
|---|---|---|
| type  | string  | Describes the step type. Can be one of the following types: extension, auth, conditional, errorCatchExtension, pipeline and staticValue  |
| input  | array\<object\>  | Defines which value of the shared object gets mapped to which key in the input object. Structure of the object is: `{"key": "<inputName>", "id": "<sharedObjectMappingId>"}`  |
| output  | array\<object\>  | Defines which output key get mapped to which id within the shared object. Structure of the object is: `{"key": "<outputName>", "id": "<sharedObjectMappingId>"}`  |
