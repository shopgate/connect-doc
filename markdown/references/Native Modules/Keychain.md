---
stoplight-id: xdev7k29x4x5w
---

# Keychain Module

The Keychain module securely stores and retrieves a username/password pair on the device.

```jsx
import { Keychain } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useState } from 'react';
import { Keychain } from '@shopgate/native-modules';

export function LoginStorage() {
  const [username, setUsername] = useState(null);
  const loadLogin = async () => {
    const credentials = await Keychain.getLogin();
    setUsername(credentials ? credentials.username : null);
  };
  return <button type="button" onClick={loadLogin}>{username ?? 'Load login'}</button>;
}
```

## setLogin(username, password)

```js
await Keychain.setLogin('user@example.com', 'password');
```

## getLogin()

```js
const credentials = await Keychain.getLogin();
```

Returns `{ username, password }` or `false` when no credentials exist.

## resetLogin()

```js
await Keychain.resetLogin();
```

`setLogin()` and `resetLogin()` resolve when complete.
