---
stoplight-id: 14x6907z1m0fo
---

# Push Module

The Push module checks notification permission and retrieves the device push token.

```jsx
import { Push } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { Push } from '@shopgate/native-modules';

export function PushTokenStatus() {
  const [token, setToken] = useState(null);
  useEffect(() => {
    const loadToken = async () => setToken(await Push.getToken());
    loadToken();
  }, []);
  return <p>{token ? 'Push enabled' : 'No push token'}</p>;
}
```

## hasPermission()

```js
const permissionGranted = await Push.hasPermission();
```

Returns `Promise<boolean>`.

## getToken()

```js
const token = await Push.getToken();
```

Returns `Promise<string | null>`.

## Events

### pushReceived

Fires when a push notification is received while it can be delivered to the web layer. The native notification payload is available as `event.detail`.

```jsx
import { useEffect } from 'react';
import { Push } from '@shopgate/native-modules';

export function PushListener() {
  useEffect(() => {
    const handlePush = (event) => console.log('Push received', event.detail);
    Push.addEventListener('pushReceived', handlePush);
    return () => Push.removeEventListener('pushReceived', handlePush);
  }, []);
  return null;
}
```
