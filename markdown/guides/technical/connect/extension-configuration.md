# Extension Configuration

This document explains how to make an extension configurable. To use this document, you need to understand extensions and the Shopgate Connect Merchant Admin.

You can make several components in your extension configurable, such as the following: 
* the color of a certain button
* timeouts for certain requests
* URLs to resources

## How extension configuration works

You define the configuration in the extension-config.json file within your extension directory. This file contains a json object, which can have the `configuration` property.


These configurations resolve to key/value pairs into multiple possible files depending on their destination:
* **backend**: `./extensions/<extensionId>/extension/config.json`
* **frontend** and of type `extension`: `./extensions/<extensionId>/frontend/config.json`
* **frontend** and of type `theme`: `./themes/<theme>/config/app.json`

When the extension is not a theme, we can use **both** as a value for the destination key. This will write the config to both frontend and backend config.json files.

| extension-config.json | config.json and/or app.json |
| --- | --- |
| "color": { some description of how to get the color value } | "color": "blue" |

Within the extension config file, the value of the configuration key represents the following:
* where the resulting value comes from (see from the Shopgate Merchant Admin, see "Configuration with Shopgate Merchant Admin")
* which files the configuration key is inserted into (config.json or app.json)

In the SDK context (when you develop your extension), each time you alter the `extension-config.json` file, the file gets resolved to `config.json` and `app.json` according to your changes.

In the application context, `config.json` and `app.json` are written while the application gets deployed.

## Types of configs

Configs consist of a key/value pair where the key is the name of the configuration and the value defines where the configuration comes from.

The following example shows the `static` type:

```json
"configuration": {
  "stage": {
    "type": "static",
    "destination": "backend",
    "params": {
      "value": "%(targetStage)s"
    }
  }
}
```

If your code is running in the sandbox environment, this configuration resolves to the following: `"stage": "sandbox"` within the backend config.json file if you set the destination to `backend`.


## Configuration with Shopgate Merchant Admin

In addition to the `static` config type, you can use the `admin` type to configure your extension.

After you insert an `admin` config type into your extension-config.json file, you can set the value of this key within the Shopgate Merchant Admin. 

> Caution: You need to release and install the extension before you can alter its configs in the Shopgate Merchant Admin. Otherwise you cannot see the extensions config.

There is no way to resolve a key that has not been released. Therefore, you need to set a default value for this key in the extension config.

Example:

```
...
"credentials": {
  "type": "admin",
  "destination": "backend",
  "params": {
    "type": "json",  // currently not supported but necessary in the future
    "label": "Credentials for the extension", // currently not supported but necessary in the future
    "required": true // currently not supported but necessary in the future
  }
}
...
```
In Extension Settings > (your extension) in the Merchant Admin, you can use a json editor to insert the configuration value as follows:

```json
{
	"credentials": {
		"user": "testUser",
		"password": "mySecurePassword123456789!?"
	}
}
```

The key needs to match the key in your extension config file.

For more info on how the `admin` type can be user refer to the admin type reference.

## Usage of Configuration Values in Extension Code


This section describes how you can access your configuration values within the extension code.

### Backend Extensions

In extension steps, you can access every config value of your extension with the `config` property of the context object.

If the credentials example above created the following config.json file:

```json
{
  "credentials": {
    "user": "testUser",
    "password": "mySecurePassword1223456789!?"
  }
}
```

you can access the value as follows:

```javascript
module.exports = async (context, input) => {
  context.log.info(context.config.credentials.user) // logs "testUser"
}
```

### Frontend Extension

The following entry within the `configuration` property of the extension-config.json:

```json
"configuration": {
  "countryCodes": {
    "type": "static",
    "destination": "frontend",
    "params": {
      "value": "DE,AT,FR,GB"
    }
  }
}
```

creates the following key/value entry within the config.json:

```json
{
  ...
  "value": "DE,AT,FR,GB"
  ...
}
```

You can access the value by importing the config and treat it as the object as follows:

```javascript
import config from './../../config'; // depending on location of this file.

const countries = config.countryCodes.split(',');

export default countries;
```

The content of the config object is the same as the content of the app.json file.

### Theme

If your extension is a theme, the config key/value pairs are resolved into the ./config/app.json of theme.

The following code shows how to access the value of the config key `colors` within theme:

```javascript
import { themeConfig } from '@shopgate/pwa-common/helpers/config';
const colors = themeConfig.colors;
```
