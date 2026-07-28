---
stoplight-id: ng60jcr0l04g7
---

# In-App Browser

The In-App Browser module opens external and SG API pages in native browser views and controls their navigation bars.

```jsx
import { InAppBrowser } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { InAppBrowser } from '@shopgate/native-modules';

export function HelpButton() {
  const openHelp = async () => InAppBrowser.showInAppBrowser({
    id: 'help',
    url: 'https://example.com/help',
    navigationBar: { pageTitle: 'Help', type: 'done' },
  });
  return <button type="button" onClick={openHelp}>Open help</button>;
}
```

```js
await InAppBrowser.showInAppBrowser({ id: 'help', url: 'https://example.com/help' });
await InAppBrowser.updateNavigationBar({ pageTitle: 'Help', type: 'done' });
await InAppBrowser.openLink({ url: 'https://example.com' });
```

Use `openSGAPIPage({ pageId, id?, ignoreCache?, navigationBar? })` for SG API pages. Navigation bar options can be passed to browser-opening methods or updated afterward.

## Events

### didOpen

Fires after an external link has opened in the native in-app browser. The event has no detail payload.

### didClose

Fires after the native in-app browser closes. The close result is available in `event.detail`.

```jsx
import { useEffect } from 'react';
import { InAppBrowser } from '@shopgate/native-modules';

export function BrowserEvents() {
  useEffect(() => {
    const handleOpen = () => console.log('Browser opened');
    const handleClose = (event) => console.log('Browser closed', event.detail);
    InAppBrowser.addEventListener('didOpen', handleOpen);
    InAppBrowser.addEventListener('didClose', handleClose);
    return () => {
      InAppBrowser.removeEventListener('didOpen', handleOpen);
      InAppBrowser.removeEventListener('didClose', handleClose);
    };
  }, []);
  return null;
}
```
