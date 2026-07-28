---
stoplight-id: bs0u0kejwboi1
---

# Android Navigation Bar Module

The Android Navigation Bar module controls the Android system navigation bar and reports device navigation and dark-mode state. Navigation-bar operations are Android-specific; state methods resolve to `undefined` on iOS.

```jsx
import { AndroidNavigationBar } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { AndroidNavigationBar } from '@shopgate/native-modules';

export function NavigationBarControls() {
  const [gestureNavigation, setGestureNavigation] = useState(null);
  const [darkMode, setDarkMode] = useState(null);

  useEffect(() => {
    const loadNavigationState = async () => {
      const [gestures, dark] = await Promise.all([
        AndroidNavigationBar.isGestureNavigationActive(),
        AndroidNavigationBar.isDarkModeActive(),
      ]);

      setGestureNavigation(gestures);
      setDarkMode(dark);
    };

    loadNavigationState();
  }, []);

  return (
    <div>
      <p>Gesture navigation: {gestureNavigation == null ? 'unknown' : String(gestureNavigation)}</p>
      <p>Dark mode: {darkMode == null ? 'unknown' : String(darkMode)}</p>
      <button
        type="button"
        onClick={() => AndroidNavigationBar.setColor({ color: '#000000' })}
      >
        Use dark navigation bar
      </button>
    </div>
  );
}
```

## setColor(params)

```js
await AndroidNavigationBar.setColor({ color: '#000000' });
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `color` | `string` | no | CSS-style color value, such as `#000000`. |

Returns `Promise<void>`.

## isGestureNavigationActive()

```js
const gestures = await AndroidNavigationBar.isGestureNavigationActive();
```

Returns `Promise<boolean | undefined>`; iOS returns `undefined`.

## isDarkModeActive()

```js
const darkMode = await AndroidNavigationBar.isDarkModeActive();
```

Returns `Promise<boolean | undefined>`; iOS returns `undefined`.
