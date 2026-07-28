---
stoplight-id: buqivdi1chmko
---

# Status Bar Module

The Status Bar module controls status-bar color, style, visibility, translucency, and network activity indicators.

```jsx
import { StatusBar } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect } from 'react';
import { StatusBar } from '@shopgate/native-modules';

export function DarkStatusBar() {
  useEffect(() => {
    const configureStatusBar = async () => {
      await StatusBar.setBarStyle({ style: 'dark-content' });
      await StatusBar.setBackgroundColor({ color: '#ffffff' });
    };
    configureStatusBar();
  }, []);
  return null;
}
```

## setBackgroundColor(params)

```js
await StatusBar.setBackgroundColor({ color: '#ffffff' });
```

## setBarStyle(params)

```js
await StatusBar.setBarStyle({ style: 'dark-content', animated: true });
```

## setHidden(params)

```js
await StatusBar.setHidden({ hidden: false, animation: 'fade' });
```

## setTranslucent(params)

```js
await StatusBar.setTranslucent({ translucent: true });
```

## getHeight()

```js
const height = await StatusBar.getHeight();
```

All setters return `Promise<void>`; `getHeight()` returns `Promise<number>`.
