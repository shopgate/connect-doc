---
stoplight-id: r5dnszes6x0rd
---

# Widget Configurations & Definitions

This page provides an overview about the widgets used in Pages 2.0, the Shopgate CMS.

## Available Widgets

The widgets that are available for your shop will depend on the Theme (PWA) version that is deployed as well as extensions.
In the Shopgate Admin, when adding a new widget, you will always see the list of available widgets for your shop.

You can also retrieve the list of available widgets via the API, see [Get Widget Config Definitions](../../../static/services/cms.yaml/paths/~1merchants~1{merchantCode}~1shops~1{shopCode}~1widgetConfigDefinitions/get).

### Example response for GET widgetConfigDefinitions

```json
{
    "meta": {
        "limit": 100,
        "offset": 0,
        "totalItemCount": 13
    },
    "widgetConfigDefinitions": [
        {
            "code": "@shopgate/widgets/imageWidget",
            "name": {
                "en-us": "Image",
                "de-de": "Bild"
            },
            "description": {
                "en-us": "Display a single image with an optional link.",
                "de-de": "Zeige ein einzelnes Bild mit optionalem Link."
            },
            "widgetConfigInputs": [
                {
                    "code": "image",
                    "label": {
                        "en-us": "Image",
                        "de-de": "Bild"
                    },
                    "required": true,
                    "type": "image",
                    "localizable": true,
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "visibilityConditions": null,
                    "typeSpecificSettings": null,
                    "defaultValue": null
                },
                {
                    "code": "useImageWide",
                    "label": {
                        "en-us": "Different image for wide screens",
                        "de-de": "Anderes Bild für breite Bildschirme"
                    },
                    "required": true,
                    "type": "boolean",
                    "localizable": false,
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "visibilityConditions": null,
                    "typeSpecificSettings": null,
                    "defaultValue": false
                },
                {
                    "code": "imageWide",
                    "label": {
                        "en-us": "Image wide",
                        "de-de": "Bild für breite Bildschirme"
                    },
                    "required": true,
                    "type": "image",
                    "localizable": true,
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "visibilityConditions": {
                        "useImageWide": true
                    },
                    "typeSpecificSettings": null,
                    "defaultValue": null
                },
                {
                    "code": "link",
                    "label": {
                        "en-us": "Link",
                        "de-de": "Link"
                    },
                    "required": false,
                    "type": "link",
                    "localizable": true,
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "visibilityConditions": null,
                    "typeSpecificSettings": null,
                    "defaultValue": null
                },
                {
                    "code": "parallax",
                    "label": {
                        "en-us": "Parallax Scrolling",
                        "de-de": "Parallax-Scrolling"
                    },
                    "required": false,
                    "type": "boolean",
                    "localizable": false,
                    "description": {
                        "en-us": "Enables a parallax scrolling effect where the image moves at a different speed than the page itself, creating a sense of depth.",
                        "de-de": "Aktiviert einen Parallax-Scrolling-Effekt, bei dem sich das Bild mit einer anderen Geschwindigkeit als die Seite selbst bewegt und so ein Gefühl von Tiefe entsteht."
                    },
                    "defaultValue": false
                },
                {
                    "code": "borderRadius",
                    "label": {
                        "en-us": "Border Radius",
                        "de-de": "Abrundung der Ecken"
                    },
                    "required": true,
                    "type": "select",
                    "localizable": false,
                    "defaultValue": "default",
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "typeSpecificSettings": {
                        "options": [
                            {
                                "value": "default",
                                "label": {
                                    "en-us": "Default",
                                    "de-de": "Standard"
                                }
                            },
                            {
                                "value": "none",
                                "label": {
                                    "en-us": "None",
                                    "de-de": "Kein"
                                }
                            },
                            {
                                "value": "rounded",
                                "label": {
                                    "en-us": "Rounded",
                                    "de-de": "Abgerundet"
                                }
                            },
                            {
                                "value": "custom",
                                "label": {
                                    "en-us": "Custom",
                                    "de-de": "Benutzerdefiniert"
                                }
                            }
                        ]
                    }
                },
                {
                    "code": "borderRadiusCustom",
                    "label": {
                        "en-us": "Custom Border Radius",
                        "de-de": "Benutzerdefinierte Abrundung"
                    },
                    "required": true,
                    "type": "number",
                    "localizable": false,
                    "description": {
                        "en-us": "",
                        "de-de": ""
                    },
                    "visibilityConditions": {
                        "borderRadius": "custom"
                    },
                    "typeSpecificSettings": {
                        "validationMinValue": 1,
                        "validationMaxValue": 50,
                        "maxNumberOfDecimals": 0
                    },
                    "defaultValue": 16
                }
            ]
        },
        ...
    ]
}
```



## General Widget Structure
Every widget in the CMS follows a standardized structure. This structure ensures a consistent experience for both the merchant managing content in the Shopgate Admin and the developer implementing the API.

### 1. Administrative Metadata
Each widget definition includes fields used specifically for the Shopgate Admin interface to help users identify and manage content:
* **`id`**: The unique technical identifier for the widget type (e.g., `imageWidget`).
* **`name`**: A localized display name (English/German) shown to users in the CMS editor.
* **`description`**: A localized explanation of what the widget does and where it should be used.

### 2. Common Fields (Global Settings)
Every widget, regardless of its specific type, includes global configuration fields. These fields are not part of the widget config definitions, since they are always available for every widget.
* **Scheduling (`visibility`)**: Controls when a widget is visible in the app using `scheduleStartDate` and `scheduleEndDate`.
* **Temporary Toggle (`isHidden`)**: A boolean flag used to manually hide a widget from the app without deleting it or changing its schedule.
* **Layout & Spacing (`layout`)**: Defines the outer spacing of the widget using `marginTop`, `marginBottom`, `marginLeft`, and `marginRight`.

### 3. Widget-Specific Inputs (`widgetConfig`)
The `widgetConfig` object is where the unique data for a specific widget resides. Its structure is determined by the `widgetConfigInputs` defined for that widget ID.
* Each input has a `code` (id), a `type` (e.g., text, image, boolean. See [Input Types](input-types.md) for a list of all available types), and `required` status.
* Many inputs support **Localizability**, allowing different values for different languages.

---

## Image Widget Example
The Image Widget is designed to display a single static asset with flexible responsive options and depth effects.

### Configuration Inputs (`widgetConfig`)
When creating or updating a page, the `widgetConfig` object for this widget supports the following keys (as of January 2026):

| Key | Type | Localizable | Description |
| :--- | :--- | :--- | :--- |
| `image` | `image` | Yes | The URL of the primary image asset. |
| `useImageWide` | `boolean` | No | If true, the system will look for the `imageWide` asset on larger screens. |
| `imageWide` | `image` | Yes | An alternative asset used specifically for wide-screen layouts. |
| `link` | `link` | Yes | An optional Shopgate deep link or external URL. |
| `parallax` | `boolean` | No | Enables a scrolling effect where the image moves slower than the page. |
| `borderRadius` | `select` | No | Options: `default`, `none`, `rounded`, or `custom`. |
| `borderRadiusCustom`| `number` | No | Required only if `borderRadius` is set to `custom`. Accepts values 1–50. |


---

## Technical Implementation Details

### Localizability
Inputs marked as `localizable: true` (like `headline` or `text`) accept an object with multiple values, one for each `LocaleCode`.

### Visibility Conditions
Some inputs are conditional and only appear if certain criteria are met:
* **Example**: The `sliderSpeed` input in the `imageSliderWidget` is only visible if `slideAutomatic` is set to `true`.


The syntax for these conditions is based on **MongoDB Query Language (MQL)**. Developers can use standard MQL operators to define when an input should be rendered.

#### Syntax Examples:
* **Direct Equality**: `"useImageWide": true` (Shows the field only if the toggle is active).
* **Comparison Operators**: `"maxDepth": { "$gte": 2 }` (Shows the field only if the value is Greater Than or Equal to 2).


### Input Types Reference
See [Input Types](input-types.md)