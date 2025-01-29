# Tutorial: How to write a tracking extension

If you want to include a new tracking provider, or change the way our default tracking works, you can write your own extension. This extension can register for existing events that are provided by us.

This tutorial explains how to add Google Analytics as a tracking provider. 

## Prerequisites
Before you begin this tutorial, complete the following tasks:

- Review the fundamentals of the [React JavaScript library](https://reactjs.org). 
- Create a [Shopgate Developer Account](https://developer.shopgate.com/admin/login).
- Complete the Shopgate [Getting Started](https://developer.shopgate.com/introduction/getting-started) instructions.
- Complete the tutorial about portals.
- Create a frontend extension with the Shopgate CONNECT SDK.

## Creating the Tracker Provider Plugin

In the first step, create the `tracker/GATracker.js` file in the `frontend` directory of the extension.

Copy the following plugin skeleton in this file:

```javascript
// frontend/tracker/GATracker.js
import BasePlugin from '@shopgate/tracking-core/plugins/Base';

/**
 * Tracking plugin for Google Analytics.
 */
class GATracker extends BasePlugin {
  /**
   * Constructor.
   */
  constructor() {
    super('googleAnalytics'); // Applies the name of the tracking plugin that will be registered.

    this.initPlugin();
  }

  /**
   * Initiate and setup the tracking SDK.
   */
  initPlugin() {
    // initalize the tracking lib here
  }
}

export default GATracker;
```

Your tracker plugin inherits from the `BasePlugin` plugin of the Shopgate Tracking Core.
This core is responsible to dispatch all events to tracker plugins.
The Tracking Core needs the name of the plugin. In this class, you must overwrite the constructor with a custom one. The name is passed through the constructor from the BasePlugin with `super(<trackerName>)`.
Now, pass the name of the tracker. In this case, the tracker is `googleAnalytics`.

## Adding the Google Analytics library

In the next step, load the script of Google Analytics to pass events to it.

To load the script to pass events to it, copy the JavaScript snippet from the [Google Analytics developer guide](https://developers.google.com/analytics/devguides/collection/analyticsjs/) (without the script tags) and paste it into the `initPlugin` function.

The result should be as follows:
```javascript
...
  initPlugin() {
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
        (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

    ga('create', 'UA-XXXXX-Y', 'auto');
  }
...
```

### Connect the Tracking events with Google Analytics

Because the library is included, you can begin connecting all events with the Google Analytics library.

The BasePlugin provides a function to add listeners to multiple events: `this.register.<eventName>(callback)`.

You can find the list of existing events [here](/references/engage/tracking-events).

In this tutorial describes how to integrate the `pageview` event.
Add the following code to the end of the `initPlugin` function:

```javascript
// Register for events
this.register.pageview((data, raw, scope, state) => {
  ga('send', 'pageview', raw.name);
});
```

After adding the code, the function should be as follows:
```javascript
  /**
   * Initiate and setup the tracking SDK.
   */
  initPlugin() {
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
        (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

    ga('create', 'UA-XXXXX-Y', 'auto');

    // Register for events
    this.register.pageview((data, raw, scope, state) => {
      ga('send', 'pageview', raw.name);
    });
  }
```

Now the plugin is listening for the `pageview` event and provides the page name to Google Analytics.
You can add multiple events at this point.

### Register the Tracking Plugin

In the next step, register the plugin into the system.

#### Entry point
To include an entry point for the plugin, create an `index.js` file in the directory `frontend/tracker` and add the following:
```javascript
// frontend/tracker/index.js
import GATracker from './GATracker';

/**
 * Create plugin instance
 */
export default function init() {
  new GATracker();
}
```

This entry point provides an `init` function which is called by the app one time at the app start. It can start the initialization of the whole plugin.

#### Adapt extension-config.json

In the last step, add the entry point to the `extension-config.json` in the root of your extension.

The current extension it should be as follows:
```json
{
  "version": "1.0.0",
  "id": "@myAwesomeOrganization/awesome-tracking",
  "components": [

  ]
}
```

Add the following json object to the components array:
```json
{
  "id": "init",
  "path": "frontend/tracker/index.js",
  "type": "tracking"
}
```

The resulting `extension-config.json` should be as follows:
```json
{
  "version": "1.0.0",
  "id": "@myAwesomeOrganization/awesome-tracking",
  "components": [
    {
      "id": "init",
      "path": "frontend/tracker/index.js",
      "type": "tracking"
    }
  ]
}
```

The tracker is now registered and receives events from the Shopgate Framework.

### Add the configuration

The Google Analytics SDK needs the `property ID` to connect the SDK with your account.

To configure this ID in the Merchant Admin, follow the guide on [extension configuration](markdown/guides/technical/connect/extension-configuration.md).
