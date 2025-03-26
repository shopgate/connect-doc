---
stoplight-id: 1cd1jqj1qg76a
---

# More (iOS theme only)
The More page is a special iOS page which offers login/logout functionality, access to informational pages about the shop, and links to shop custom CMS pages links (if configured).

## How to customize
### Portals
Main portals available on the More page are listed on [NavMenu portals reference page](../portals/navmenu.md).

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';

const Component = () => (
    <Link href="/more">Open more page</Link>
);

export default Component;
```