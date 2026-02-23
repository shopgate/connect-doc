---
stoplight-id: ie3px6d0msilv
---

# Requesting App Permissions

Modern mobile operating systems require explicit user consent before an app can access privacy-sensitive features. Permissions are necessary to ensure transparency and give users control over how their data and device capabilities are used.

Within the app, the following permissions are supported:
- Geolocation
- Camera
- Push Notifications
- App Tracking Transparency (iOS only)

Mobile operating systems strictly regulate when and how permission dialogs may be presented. The process of obtaining a permission typically involves multiple steps and requires coordination between the JavaScript layer and the native application.

To abstract platform-specific differences (iOS vs. Android) and simplify this workflow, we provide a set of `Redux actions` that encapsulate the required native communication, permission state evaluation, and decision logic.

All actions can be imported from `@shopgate/engage/core/actions`.

## Available Redux Actions

The following Redux actions are available to request app permissions from within the React application:

```js
import {
  grantGeolocationPermission,
  grantPushPermissions,
  grantCameraPermission,
  grantAppTrackingTransparencyPermission
} from '@shopgate/engage/core/actions';
```
Each action checks the current permission status, triggers a native permission dialog if allowed by the OS
and resolves with the resulting permission state.

The actions need to be dispatched via `dispatch` from `react-redux`. They return a `Promise` that resolves with data that describes the outcome of the request.

```js
import { useDispatch } from 'react-redux';

// Code inside a React component
const dispatch = useDispatch();
const success = await dispatch(grantGeolocationPermission())
```

To get an overview about the available options for the actions, check [Action Options](#action-options). For example implementations go to [Examples](#examples).

The `grantAppTrackingTransparencyPermission` is only supported on iOS right now. Its return value will always indicate a success when permission is requested on Android.

### Action Options

| Option | Description | Type | Default |
|--------|-------------|------|---------|
|`resolveWithData`| If set to `true` the promise will resolve with an object containing the permission status and additional data, instead of a boolean value. (see [Grant Permissions Resolved Value](#grant-permissions-resolved-value))| `[boolean]`| `false` |
|`useSettingsModal` | Whether in case of declined permissions a modal shall be presented, which redirects to the app settings. | `[boolean]`| `false`|
|`settingsModal`| Options for the settings modal (see [Modal Options](#modal-options)). In version < 7.30.1 this option was called `modal`. From 7.30.1 this option is flagged as deprecated. | `[object]`| `{}` |
|`useRationaleModal` | Whether a rationale modal should be shown before requesting the permission. | `[boolean]`| `false` |
|`rationaleModal`| Options for the rationale modal (see [Modal Options](#modal-options)). | `[object]`| `{}` |
|`requestPermissions`|If set to `true` no permissions will be requested if not already granted. Otherwise only the current permission status will be checked without prompting the user.| `[boolean]`| `false` |
|`requireBackgroundAccess`|Only available for `grantGeolocationPermission`.<br/>Whether to request background location access.<br />Since background location access will cause extended reviews by Google and Apple, this feature needs to be explicitly enabled by Shopgate.| `[boolean]`| `false` |

#### Modal Options
Possible options for `modal` and `rationaleModal` objects

| Option | Description | Type | Default |
|--------|-------------|------|---------|
|`title`| Modal title (will can be omitted when set to `null`) | `[string]` | `null` |
|`message`| Modal message | `string` | Depends on the permission type. |
|`confirm`| Label for the confirm button | `[string]` | `permissions.access_denied.settings_button` for settings modal |
|`dismiss`| Label for the dismiss button | `[string]` | `modal.dismiss` for settings modal |
|`params`| Additional parameters for i18n strings | `[object]` || |

#### Grant Permissions Resolved Value
When `resolveWithData` is set to `true`, the action will resolve with an object of the following shape. Otherwise with a `boolean` value that indicates if the permission was successfully granted.

| Option | Description | Type |
|--------|-------------|------|
|`success`| Whether the permission was successfully granted | `boolean` |
|`status`| The current permission status | `"granted" \| "denied" \| "notDetermined" \| "notSupported"` |
|`optInRequested`| Whether an a permission dialog was shown during the process | `boolean` |

## Examples

### React component example

The component below will preset a geolocation permission dialog with custom translations when the user didn't opt-in yet.

```jsx
import { useCallback } from 'react';
import { useDispatch } from 'react-redux';
import { grantGeolocationPermission } from '@shopgate/engage/core/actions';
import { Button } from '@shopgate/engage/components';

const MyComponent = () => {
  const dispatch = useDispatch();

  const handleClick = useCallback(async () => {
    const { success, status } = await dispatch(grantGeolocationPermission({
      resolveWithData: true,
      useSettingsModal: true,
      modal: {
        title: 'my.title.from.translations',
        message: 'my.message.from.translations'
      }
    }))
  }, [dispatch]);

  return (
    <Button onClick={handleClick}>
      Allow Geolocation Access
    </Button>
  )
};

export default MyComponent;
```

### RxJS Subscription Example

The subscription below will preset a geolocation permission dialog on app start with custom translations when the user didn't opt-in yet.

```js
import { appWillStart$ } from '@shopgate/engage/core/streams';
import { grantPushPermissions } from '@shopgate/engage/core/actions';

export default function mySubscriptions(subscribe) {
  subscribe(appWillStart, async ({ dispatch }) => {
    const { success, status } = await dispatch(grantPushPermissions({
      resolveWithData: true,
      useSettingsModal: true,
      modal: {
        title: 'my.title.from.translations',
        message: 'my.message.from.translations'
      }
    }))
  });
}
```

## Bonus: Retrieve the User’s Geolocation

To simplify access to the user’s current location, we provide the `getGeolocation` Redux action. This action combines permission handling and location retrieval into a single workflow.

### Options

The available options are equal to the [Action Options](#action-options) used by the permission request action, with one exception:
- `resolveWithData` is **not supported** since the action resolves with location data on success.

When the action is dispatched, the current geolocation permission status is evaluated, if necessary and allowed by the OS, a native permission dialog is triggered, if permission is granted, the device’s current location is requested and the action Promise will resolve with an object that contains location data (`latitude`, `longitude` and `accuracy`).

If the permission was denied, the returned Promise rejects with an error.

```jsx
import { useCallback } from 'react';
import { useDispatch } from 'react-redux';
import { getGeolocation } from '@shopgate/engage/core/actions';
import { Button } from '@shopgate/engage/components';

const MyComponent = () => {
  const dispatch = useDispatch();

  const handleClick = useCallback(async () => {
    try {
      const { latitude, longitude, accuracy } = await dispatch(getGeolocation({
        useSettingsModal: true,
        modal: {
          title: 'my.title.from.translations',
          message: 'my.message.from.translations'
        }
      }));
    } catch (e) {}
  }, [dispatch]);

  return (
    <Button onClick={handleClick}>
      Located Me
    </Button>
  )
};

export default MyComponent;
```