# Extension Config

The extension config contains information about its extension. It is located on the root level of an extension as `extension-config.json`. It consists of the following main properties:


| Name | Type | Required | Description |
|--|--|--|--|
| **id** | string | yes | Indicates the extension id, such as: "@shopgate/products" |
| **version** | string | yes | Indicates semver version of the extension, such as "1.0.0" |
| **trusted** | boolean | no | Indicates whether the extension is trusted |
| **configuration** | object | no | Configures frontend / backend parts |
| **components** | array | no | Lists available frontend components for this extension |
| **steps** | array | no | Lists available steps that hook into pipeline hook steps |

Minimal example:

```json
{
  "id": "@shopgate/products",
  "version": "1.0.0",
  "trusted": false
}
```
## Configuration Property
The configuration property is an object with the following structure:
```json
{
  <configKey>: <configDescription>
}
```

### Configuration description

The configuration description is an object that determines the targets of the config and where the information comes from. The description consists of the following properties:


| Property Name | Type | Required |  Description |
|--|--|--|--|
| **type** | string | yes | Describes where the resulting value comes from; available types are `admin`, `static` |
| **destination** | array of strings | yes | Includes `frontend` (`./themes/<theme>/config/app.json` or `./extensions/<extensionId>/frontend/config.json`), `backend`(`./extensions/<extensionId>/extension/config.json`), or `both` |
| **params** | object | yes | Describes how the value is fetched; depends on the selected type |
| **default** | any | no | Defines the value of the resolved key if the described way in params fails |

#### Static Type

With the static type, you can define the value of your configuration directly in the extension-config.json. Getting the value  can not fail so you don't need the `default` property in that case.

The **param** property object of the static type needs only the `value` key.

If the `value` property of `param` is a string or an object containing strings, these strings can include certain placeholders which also get resolved. The following placeholders are available:


| Name | Type | Description |
|--|--|--|--|
| **appId** | string | Indicates your current app id, such as "app_123456" |
| **publicPath** | string | Indicates the base path where your application is served |
| **themes** | array of strings | Shows the available themes, including their versions |
| **themeMapping** | object | Contains keys such as "app_android_phone" with a mapped theme id |
| **targetStage** | string | Identifies either `production` or `sandbox`|
| **extensionId** | string | Provides the id of the current extension |

The pattern of a replacement is `%(<placeholder>)s` such as `%(appId)s`.

Example:

```json
"metaData": {
  "type": "static",
  "destination": "backend",
  "params": {
    "value": {"publicPath": "%(publicPath)s", "fields": ["firstName", "lastName", "street1", "street2", "zipCode", "city", "country"]}
  }
},
```

The above example code resolves to the following :

```json
"addressFields": {"publicPath": "https://connect.shopgate.com/shop_12345/@shopgate/theme-gmd/5.6.0/index.html", "fields":["firstName", "lastName", "street1", "street2", "zipCode", "city", "country"]}
```

#### Admin Type

The admin type enables you to insert configuration values set within the Shopgate CONNECT Merchant Admin. It creates an input within the Shopgate Merchant Admin to set its value.

The value input can be displayed in several different forms, such as text fields, checkboxes, and more. . To configure the admin type you have to set a subtype along with its specific options:

##### Subtypes

Each subtype has to be described in the `params` property of the admin type. The admin type consists of the following properties:


| Name | Type | Required | Description |
|--|--|--|--|
| **type** | string | yes | Indicates whether it is a `json`, `text`, `textarea`, `color`, `checkbox`, `number` or `select` subtype |
| **label** | string | yes | Displays the  text for the configuration within the Shopgate Connect Merchant Admin |
| **description** | string | no | Displays the description text for the configuration within the Shopgate Connect Merchant Admin |
| **default** | any | no | Indicates the default value for the config (if not required) |
| **required** | boolean | no | Indicates, as a boolean,  whether the config MUST be configured |
| **options** | object | no | Provides custom configuration options based on the type property |

Example:

```json
"configWithCustomName": {
  "type": "admin",
  "destination": "backend",
  "default": {
    "foo": "bar"
  },
  "params": {
    "type": "json",
    "label": "Config C (json)",
    "required": true,
  }
}
```

**Available Subtypes**

* **json**: Creates a text area for json content.

  Possible values: Any json compatible object which will be configurable in json code editor.

  Returns: object

* **text**: Creates a single line text area.

  Possible values: Any string / text content that can be inserted in a single line.

  Options:
  * placeholder: optional placeholder text

  ```json
  "options": {
    "placeholder": "place the url here"
  }
  ```

  Returns: string

* **textarea**: Creates a multiline text area.

  Possible values: Any string / text content that can be inserted in a single line.

  Options:
  * placeholder: optional placeholder text
  * rows: optional row count to display

  ```json
  "options": {
    "placeholder": "place your text here",
    "rows": 6
  }
  ```

  Returns: string

* **color**: Creates a color picker.

  Returns: CSS compatible value

* **checkbox**: Creates a checkbox.

  Options:
  * label: Provides label for the checkbox input.

  ```json
  "options": {
    "label": "enable logs"
  }
  ```

  Returns: boolean

* **number**: Creates an input of the type number.

  Options:
  * min: optional minimal value of the number
  * max: optional maximum value of the number

  ```json
  "options": {
    "min": "0",
    "max": "15"
  }
  ```

  Returns: number

* **select**: Creates a selected input.

  Options:
  * multiple: boolean indicating if multiple selections are possible
  * options: array of objects<label, value>

  ```json
  "options": {
    "multiple": false,
    "options": [
      {"label": "one", "value": 1}
      {"label": "two", "value": 2}
    ]
  }
  ```

  Returns: any value, if not multiple, array of values if multiple selection is enabled

**Note:** The Shopgate CONNECT Merchant Admin currently does not support the display of inputs, but future releases plan to support that feature. Use the Admin type subtypes to comply with that future change.

## Components Property

The component property is a list of all frontend components provided by this extension. These components are portals, subscribers, reducers, widgets, and translations.

Within the extension config file, a component definition has the following properties:


| Name | Type | Description |
|--|--|--|
| **id** | string | Indicates the id of the component (needs to be unique within the component) |
| **path** | string | Shows the path to the component (relative from the extension root folder) |
| **type** | string | Indicates the type of the component (portals, subscribers, reducers, widgets, or translations) |
| **target** | string or array of string | Indicates the target for only type "portals". Refer to the portals reference for information about using portals type. |

Example:

```json
"components": [
  {
    "id": "UserRoutes",
    "path": "frontend/pages/routes.jsx",
    "target": "app.routes",
    "type": "portals"
  },
  {
    "id": "en-US",
    "path": "frontend/locale/en-US.json",
    "type": "translations"
  },
  {
    "id": "de-DE",
    "path": "frontend/locale/de-DE.json",
    "type": "translations"
  },
  {
    "id": "UserSubscribers",
    "path": "frontend/subscriptions/index.js",
    "type": "subscribers"
  },
  {
    "id": "UserReducers",
    "path": "frontend/reducers/index.js",
    "type": "reducers"
  }
]
```

## Steps property

Step definitions consist of the following properties:


| Name | Type | Required | Description |
|---|---|---|---|
| **path** | string | yes | Provides path to the extension step, including the "extension" folder |
| **description** | string | no | Describes briefly what the step does and what a system integrator needs to know to properly place it in the pipeline(s) |
| **hooks** | array of strings | yes | the targets property describes where the step should be inserted (list of hook strings) |
| **input** | array of objects | no | Indicates input of the step; if the step is made for a hook, the names need to match the input's name of the hooks |
| **output** | array of objects | no | Indicates output of the step; within the step code, align property names of your returned object to match those defined here |

### Hook String

A hook string consists of the pipeline name and a hook name, separated by a colon. The hooks are defined in the `target` key on every step. If the step should not be included in a hook, the array can be empty or the target can be removed.

The hook string schema is as follows:

```json
{pipelineName}:{hookName}
```

To have a step included in all hooks of a certain name, regardless of the pipeline, use the asterisk wildcard as pipeline name as shown in following the example:

```json
*:{hookName}
```

**Note:** Steps are always and only included in hooks of pipelines of the same trust level (trusted/untrusted).

### Dynamic Input And Output

You might need to work with additional input values or add additional keys to the output.

#### Input

To add additional input values, define those as objects in the `inputs` array. Input objects have the following properties:


| Name | Type | Required | Description |
|---|---|---|---|
| **key** | string | yes | Indicates key of the input |
| **addPipelineInput** | boolean | no | Defines whether the input should be added to the pipeline's input array |
| **optional** | boolean | no | Defines whether the input is required (false) or optional (true) in case it is added to the pipeline input (`addPipelineInput` is true) |
| **internal** | boolean | no | Defines whether the input is internal for the extension; only inserted steps of the extension have access to this input |

Example:

```json
"input": [{
  "key": "someInternalInput",
  "internal": true
}, {
  "key": "somePipelineInput",
  "optional": true
}, {
  "key": "someAdditionalInput",
  "addPipelineInput": true,
  "optional": true
}]
```

#### Output

To add additional output values, define those as objects in the `outputs` array. Output objects have the following properties:


| Name | Type | Required | Description |
|---|---|---|---|
| **key** | string | yes | key of the output |
| **addPipelineOutput** | boolean | no | Defines whether the output should be added to the pipeline's output array |
| **optional** | boolean | no | Defines whether the output is required (false) or optional (true) in when the flag `addPipelineOutput` is true |
| **internal** | boolean | no | Defines whether the output is internal for the extension; only inserted steps of the extension have access to this input |

```json
{
  "key": "someOutput",
  "optional": true,
  "addPipelineOutput": true
}
```
