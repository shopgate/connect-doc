---
stoplight-id: ivmws1hpfe55b
---

# HTTP Module

The HTTP module performs native HTTP requests and can synchronize cookies between the request and the app's cookie store.

```jsx
import { Http } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { Http } from '@shopgate/native-modules';

export function ItemCount() {
  const [count, setCount] = useState(null);
  useEffect(() => {
    const loadItems = async () => {
      const response = await Http.httpRequest({ url: 'https://api.example.com/items' });
      setCount(Array.isArray(response.body) ? response.body.length : 0);
    };
    loadItems();
  }, []);
  return <p>Items: {count ?? 'Loading…'}</p>;
}
```

## httpRequest(params)

```js
const response = await Http.httpRequest({
  url: 'https://api.example.com/items',
  method: 'GET',
  timeout: 30000,
  synchronizeCookies: true,
});
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `url` | `string` | yes | Request URL. |
| `method` | `string` | no | HTTP method; defaults to `GET`. |
| `headers` | `object` | no | Request headers. |
| `body` | `unknown` | no | Request body. |
| `timeout` | `number` | no | Timeout in milliseconds. |
| `followRedirects` | `boolean` | no | Follow redirects; defaults to `true`. |
| `synchronizeCookies` | `boolean` | no | Synchronize native cookies. |

### Return value

The response contains `headers`, `statusCode`, and a parsed or raw `body`.

## setCookie(params)

```js
await Http.setCookie({
  name: 'session',
  value: 'abc',
  domain: 'example.com',
});
```
