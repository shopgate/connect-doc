---
stoplight-id: s229hyi2s4y63
---

# Implement a Cuatom widget

## Introduction

Widgets are predefined content blocks for the Shopgate CMS or "Pages System", which enables merchants to design their own pages quickly and easily. By default, Shopgate provides the following widget types:
* Image
* Image Slider
* Hero Banner
* Video
* Button
* Headline
* Rich Text
* Category List
* Product List
* Product Slider
* Custom HTML

This guide will show you how to implement your own widget.

## Implementation

Every widget is a React component which is dynamically rendered into a CMS page.

### 1. Creating a widget component

In the first step, you need to create a React component for your widget.
Create the file `/frontend/myAwesomeWidget/index.jsx` in your extension
with the following content:

```javascript
import React from 'react';

class MyAwsomeWidget extends React.Component {
  /**
   * Renders the component.
   * @returns {JSX}
   */
  render() {
    // render your content here
  }
}

export default MyAwsomeWidget;
```

### 2. Using the widget settings

In the Shopgate Merchant Admin, the merchant can configure settings for widgets on an individual basis. These settings are passed as a `settings` prop into the component. It can be used to adapt the widget's design or specify how data is fetched.

Because one type of widget can exist multiple times on the same page, the settings differ per instance of the widget.

`Settings` is always an object and can contain every kind of key/value pairs of the type string, number, object and array.

The following example shows how to access the setting `title` in a widget:

```javascript
import React from 'react';

class MyAwsomeWidget extends React.Component {
  /**
   * Renders the component.
   * @returns {JSX}
   */
  render() {
    return (
      <h1>{this.props.settings.title}</h1>
    );
  }
}

export default MyAwsomeWidget;
```

### 3. Register widget in the extension-config.json

To connect the widget with the theme, you need to adjust the `extension-config.json`.
Add the following object into the `components` array of the config:

```json
{
  "id": "MyAwesomeWidget",
  "path": "frontend/myAwesomeWidget/index.jsx",
  "type": "widgets",
  "description": "My Awesome Widget"
}
```

Your extension can contain multiple widgets, therefore it is important to note that the widget id must be unique within the extension.

After the change, the `extension-config.json` should look like this:
```json
{
  "version": "1.0.0",
  "id": "@myAwesomeOrganization/someWidgets",
  "components": [
    {
      "id": "MyAwesomeWidget",
      "path": "frontend/myAwesomeWidget/index.jsx",
      "type": "widgets",
      "description": "My Awesome Widget"
    }
  ],
  "configuration": {

  }
}
```

The widget is now successfully registered and can be configured in the Merchant Admin.

> **Note:** 
>
>Please make sure you restart the frontend part of the Platform SDK when you add a new widget.

## Configuration

To configure the widget, login into the [Merchant Admin](https://admin.shopgate.com) and navigate to the Pages section (Design -> Pages).

### 1. Add a new widget

To configure a new custom widget, create a new `HTML / Text Editor` widget.

Copy the following configuration into the HTML editor field to activate your widget:

```htmlmixed
<!--Widget
{
  "type": "@myAwesomeOrganization/someWidgets/MyAwesomeWidget",
  "settings": {
    "title": "This is the title of my awesome widget"
  }
}
-->
```

The configuration contains a JSON with the keys `type` and `settings`.
The `type` is a combination of the extension name ("@myAwesomeOrganization/someWidgets") and the widget id ("MyAwesomeWidget").

The `settings` object is what gets passed into the React component.

> **Note:**
>
> Please make sure that the JSON is surrounded by `<!--Widget` and `-->`.

### 2. Publish changes
As a last step, save the widget and publish the changes with the `Publish` button on the main page.
Your changes will be applied immediately to the system.

To test your widget, simply navigate to the page you added it to in your test environment.

