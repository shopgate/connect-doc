---
stoplight-id: ezsxlpwcufmzk
---

# Splash Screen Module

The Splash Screen module shows or hides the native launch splash screen.

```jsx
import { SplashScreen } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect } from 'react';
import { SplashScreen } from '@shopgate/native-modules';

export function AppReady() {
  useEffect(() => {
    const hideSplashScreen = async () => SplashScreen.hide();
    hideSplashScreen();
  }, []);
  return null;
}
```

## hide()

```js
await SplashScreen.hide();
```

## show()

```js
await SplashScreen.show();
```

Both methods return `Promise<void>`.
