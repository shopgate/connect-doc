---
stoplight-id: x3ox0pxo2avf9
---

# Sharing Module

The Sharing module opens the platform share sheet with a message and optional URL or title.

```jsx
import { Sharing } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { Sharing } from '@shopgate/native-modules';

export function ShareButton() {
  return (
    <button type="button" onClick={() => Sharing.shareItem({ message: 'Hello from the app' })}>
      Share
    </button>
  );
}
```

## shareItem(content)

```js
await Sharing.shareItem({
  message: 'Check this out',
  url: 'https://example.com',
  title: 'Example',
});
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `message` | `string` | yes | Message to share. |
| `url` | `string` | no | URL to share; iOS-specific. |
| `title` | `string` | no | Share title; Android-specific. |

Returns `Promise<void>`.
