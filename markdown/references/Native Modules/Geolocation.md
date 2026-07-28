---
stoplight-id: zip6arf7yeks7
---

# Geolocation Module

The Geolocation module configures native location services, requests authorization, and reads the device's current position.

```jsx
import { Geolocation } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useState } from 'react';
import { Geolocation } from '@shopgate/native-modules';

export function LocateButton() {
  const [position, setPosition] = useState(null);
  const locate = async () => {
    await Geolocation.requestAuthorization();
    setPosition(await Geolocation.getCurrentPosition());
  };
  return <button type="button" onClick={locate}>{position ? 'Located' : 'Locate me'}</button>;
}
```

## setConfiguration(config)

```js
await Geolocation.setConfiguration({ authorizationLevel: 'whenInUse' });
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `skipPermissionRequests` | `boolean` | no | Prevent automatic permission requests. |
| `authorizationLevel` | `string` | no | `whenInUse`, `always`, or `auto`. |

## requestAuthorization()

```js
await Geolocation.requestAuthorization();
```

## getCurrentPosition(params)

```js
const position = await Geolocation.getCurrentPosition({ enableHighAccuracy: true });
```

`getCurrentPosition()` returns a native geolocation position with latitude, longitude, accuracy, and related coordinates.
