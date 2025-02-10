---
stoplight-id: bs4v1hg2hg9j4
---

# Client Selectors

* [getDeviceInformation](#getdeviceinformation)
* [getPlatform](#getplatform)
* [getOSVersion](#getosversion)
* [getDeviceModel](#getdevicemodel)
* [isAndroid](#isandroid)
* [isIos](#isios)

## getDeviceInformation

Retrieves the device information from the client information in the store.

### Usage

```javascript
import { getDeviceInformation } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getDeviceInformation } from '@shopgate/pwa-common/selectors/client'`

### Parameters

* `state` _(Object)_ *required*: The application state.

### Returns

_(Object|null)_: The device information. If no device information is found, it returns `null`.

### Example
The following device information was taken from a Samsung Galaxy S8 with Android 8. The data is usually provided by the native part of Engage. Within the browser environment you will receive a reduced version of the object with mocked data which is based on the User Agent.

```javascript
{
  advertisingId: '0c882fb3-3254-445d-b662-e0e61cf83976',
  cameras: [
    {
      light: true,
      resolutionX: 4032,
      resolutionY: 3024,
      type: 'back',
      video: true
    },
    {
      light: false,
      resolutionX: 3264,
      resolutionY: 2448,
      type: 'front',
      video: true
    }
  ],
  carrier: 'T-Mobile',
  locale: 'en',
  model: 'SM-G950F',
  os: {
    apiLevel: '26',
    platform: 'android',
    ver: '8.0.0'
  },
  screen: {
    height: 2768,
    scale: 4,
    width: 1440
  },
  type: 'phone'
}
```
---

## getPlatform

Retrieves the platform for the device from the client information in the store.

### Usage

```javascript
import { getPlatform } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getPlatform } from '@shopgate/pwa-common/selectors/client'`

### Parameters

* `state` _(Object)_ *required*: The application state.

### Returns

_(string|null)_: The platform information. Possible values `ios` and `android`. If no platform information is found, it returns `null`.

---

## getOSVersion

Retrieves the operating system version from the client information in the store.

### Usage

```javascript
import { getOSVersion } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getOSVersion } from '@shopgate/pwa-common/selectors/client'`

### Returns

_(string|null)_: The OS version. The format depends on the device and OS (e.g. "12.3" or "8.0.0"). If no OS version is found, it returns `null`.

---

## getDeviceModel

Retrieves the device model from the client information in the store.

### Usage

```javascript
import { getDeviceModel } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getDeviceModel } from '@shopgate/pwa-common/selectors/client'`

### Parameters

* `state` _(Object)_ *required*: The application state.

### Returns

_(string|null)_: The device model (e.g. "SM-G950F" or "iPhone11.0"). If no device model information is found, it returns `null`.

---

## isAndroid

Retrieves whether the platform is “Android” from the client information in the store.

### Usage

```javascript
import { isAndroid } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isAndroid } from '@shopgate/pwa-common/selectors/client'`

### Parameters

* `state` _(Object)_ *required*: The application state.

### Returns

_(boolean)_: Whether the platform is Android.

---

## isIos

Retrieves whether the platform is iOS from the client information in the store.

### Usage

```javascript
import { isIos } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isIos } from '@shopgate/pwa-common/selectors/client'`

### Parameters

* `state` _(Object)_*required*: The application state

### Returns

_(boolean)_: Whether the platform is iOS.