---
stoplight-id: 5zf1ibzawifsr
---

# Linking Module

The Linking module opens a URL outside the app's main web view.

```jsx
import { Linking } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { Linking } from '@shopgate/native-modules';

export function ExternalLinkButton() {
  return (
    <button type="button" onClick={() => Linking.openPageExtern({ src: 'https://example.com' })}>
      Open website
    </button>
  );
}
```

## openPageExtern(params)

```js
await Linking.openPageExtern({ src: 'https://example.com' });
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `src` | `string` | yes | URL to open externally. |

Returns `Promise<void>`.

## Events

### universalLinkOpened

Fires when an HTTPS universal link is opened. The destination URL is available as `event.detail.link`.

### deepLinkOpened

Fires when a non-HTTP deep link is opened. The destination URL is available as `event.detail.link`.

```jsx
import { useEffect } from 'react';
import { Linking } from '@shopgate/native-modules';

export function LinkListener() {
  useEffect(() => {
    const handleLink = (event) => console.log('Opened link', event.detail.link);
    Linking.addEventListener('universalLinkOpened', handleLink);
    Linking.addEventListener('deepLinkOpened', handleLink);
    return () => {
      Linking.removeEventListener('universalLinkOpened', handleLink);
      Linking.removeEventListener('deepLinkOpened', handleLink);
    };
  }, []);
  return null;
}
```
