---
stoplight-id: j1jdsqjmsscv7
---

# Connectivity Monitor Module

The Connectivity Monitor reports whether the device is connected and identifies the active connection type.

```jsx
import { ConnectivityMonitor } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { ConnectivityMonitor } from '@shopgate/native-modules';

export function ConnectionStatus() {
  const [state, setState] = useState(null);
  useEffect(() => {
    const loadState = async () => setState(await ConnectivityMonitor.getCurrentConnectivityState());
    loadState();
  }, []);
  return <p>{state ? `${state.type}: ${state.connected ? 'online' : 'offline'}` : 'Loading…'}</p>;
}
```

## getCurrentConnectivityState()

```jsx
const readConnectivity = async () => {
  const state = await ConnectivityMonitor.getCurrentConnectivityState();
  // { connected: true, type: 'WIFI' }
};
```

### Return value

Returns `{ connected: boolean | null, type: string | null }`. `type` is `WIFI`, `2G`, `3G`, `4G`, `UNKNOWN`, or `null` when disconnected.

## Events

### onConnectivityStateChange

`onConnectivityStateChange` fires whenever the device's connectivity state changes. The state is provided in `event.detail`.

| Property | Type | Description |
|----------|------|-------------|
| `event.type` | `string` | Always `onConnectivityStateChange`. |
| `event.detail.connected` | `boolean \| null` | Whether the device is connected. |
| `event.detail.type` | `string \| null` | `WIFI`, `2G`, `3G`, `4G`, `UNKNOWN`, or `null`. |

```jsx
import { useEffect, useState } from 'react';
import { ConnectivityMonitor } from '@shopgate/native-modules';

export function LiveConnectionStatus() {
  const [state, setState] = useState(null);

  useEffect(() => {
    const handleConnectivityChange = (event) => {
      setState(event.detail);
    };

    ConnectivityMonitor.addEventListener('onConnectivityStateChange', handleConnectivityChange);
    return () => {
      ConnectivityMonitor.removeEventListener('onConnectivityStateChange', handleConnectivityChange);
    };
  }, []);

  return <p>{state ? `${state.type}: ${state.connected ? 'online' : 'offline'}` : 'Waiting for connectivity'}</p>;
}
```

The event detail has the same shape as `getCurrentConnectivityState()`: `{ connected, type }`.
