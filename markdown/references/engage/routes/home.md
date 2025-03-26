---
stoplight-id: 2ukkjaxvkq7cg
---

# Index (home) / CMS Pages
Index page (home) and CMS pages are essentially the same type of content, which uses the same components. Both routes contain `AppBar` and `TabBar` (iOS theme). The content is a set of Widgets which are configured in the Merchant Area.


## How to customize content
### Custom widgets
Shopgate Engage provides some widgets out of the box, but you can [create a custom one](/custom-widgets). When creating a new feature that can be customized in a WYSIWYG manner, always consider the custom widgets approach, since it gives you the following additional benefits:
- Your user (editor) is able to add basic widgets like `HTML Widget` or `Image Widget` before and after a custom widget.
- Your user (editor) is free to include your custom widget in any CMS page or home page.
- There is no need to redeploy the shop in order to update the content of a CMS or Index page.

### Portals
Index page portals can be found on a [CMS portal documentation pages](../portals/cms-pages.md)

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { INDEX_PATH } from '@shopgate/engage/core';

const Component = () => (
    <Link href={INDEX_PATH}>Go back to home page</Link>
);

export default Component;
```

There are no path name constants for CMS pages, since those pages are configured in the Merchant Area and each shop has its own linking structure. The pattern for all pages is `/page/:pageId`.

In order to link to a known page for your extension, simply provide a string to an `href` prop.
```jsx
const Component = () => (
    <Link href="/page/my-custom-page">Open my custom page</Link>
);
```