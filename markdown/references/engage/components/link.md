---
stoplight-id: wag28udlo4b2i
---

# Link
Manages linking within the Shopgate Engage App.

## Purpose
The `Link` component manages different URL types within the app for the developer.

The `Link` component detects if the provided `href` prop is an internal or external link. This component also handles special links that have varied implementation between shops, like `/checkout`.

## Usage

### Internal linking
When your component links to any internal page provided by the theme, it is always best to use [Route Constants](/references/engage/routes).

We recommend using path constants when linking to an internal page provided by an extension.

```jsx
import { Link } from '@shopgate/engage/components';
import { CART_PATH } from '@shopgate/engage/cart'

const Component = () => (
    <Link href={CART_PATH}>
        Cart page
    </Link>
);

export default Component;
```

This produces the following HTML:
```html
<div class="internal-theme-class" role="link">
    Cart page
</div>
```

### External linking
When your component links to an external URL, you only need to provide an `href` prop. The `Link` component automatically detects that it is an external link and handles the opening in an In-App browser.

Example (In-App browser):
```jsx
import { Link } from '@shopgate/engage/components';

const Component = () => (
    <Link href="https://example.com">
        Example external page
    </Link>
);

export default Component;
```

In order to open an external link in an In-App browser, you can force a link handler to pass the link directly to the system. This is an effective way of linking to an external service, in case the customer actively uses that service.

For example, it is most likely that a customer is already logged in to popular messaging apps in iOS Safari. By forcing the system to open the link, you allow the OS to bring the customer to the correct place.

Example (System browser / Universal Link):
```jsx
import { Link } from '@shopgate/engage/components';

const Component = () => (
    <Link href="https://example.com" state={{ target: '_blank' }}>
        Example external page (link will be handled by OS)
    </Link>
);

export default Component;
```

## Props
| Name | Type | Default | Description |
| - | - | - | - |
| __children__* | node | | The link content |
| __href__ * | string | | Internal pathname or external link (e.g. https, tel, mailto) |
| className | string | | Additional CSS class name |
| disabled | bool | `false` | Whether component should appear disabled |
| replace | bool | `false` | Whether onclick should replace current page (internal pages only) |
| state | Object | `{}` | [Route state](/references/engage/actions/router) |
| tag | string | `div` | HTML tag used as a link wrapper |