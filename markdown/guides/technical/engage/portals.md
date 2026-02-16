## What are Portals?

You can customize your app by modifying a Shopgate theme with portals. You use a portal to add, replace, or remove React components from a theme using an extension. Use portals to customize the existing theme without having to fork or build your own. However, for extensive customizations, we recommend creating your own theme.

## Portal Types: Parents and Siblings
There are two types of portals: parents and siblings. You use a parent portal to wrap around and replace an existing React component. You use a sibling portal to inject new components above or below an existing React component.

## Portal Names

Portals have unique names, and portal names use the following naming convention: `<feature>.<content>.<position (optional)>`. Sibling names always include a position suffix in their names.

Parent portal name example: `PRODUCT-ITEM.NAME`

Sibling portal name example: `PRODUCT-ITEM.NAME.AFTER`

Refer to the [Portals Reference](../../../references/engage/portals/index.md) for a list of available portals.

## How to Add a Component using a Portal

1. Open the `extension-config.json` file at the root of your extension.
2. Add the following code to the components array.
3. Make sure that your extension is attached and the SDK is running.

**extension-config.json**
```json
{
    "id": "MyComponent",
    "path": "frontend/MyComponent/index.jsx",
    "target": "product-item.name.before",
    "type": "portals"
}
```

| Code     | Definition                                                                                                                                                           |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`     | Unique id for this portal component. Must be unique within this extension.                                                                                           |
| `path`   | Relative path to the component that renders inside the portal. Path must include the file extension, and the file it references must export a valid React component. |
| `target` | Name of the portal to use.                                                                                                                                           |
| `type`   | Must be `portals`.                                                                                                                                                   |

4. Verify that your component, MyComponent, appears at the position of the `product-item.name.before` portal.

## How to Create a New Page with Portals

To create a new page you can use the `app.routes` portal. This portal gives you a `View` component as a prop which you can use to render the page. To do this you must create a new component in your extension:

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import { Route } from '@shopgate/engage/components';

class MyPageComponent extends React.Component {
  render() {
    const { View } = this.props;
    return (
      <View>
        <div>Hello, I'm a page.</div>
      </View>
    );
  }
}

const MyRoute = props => (
  <Route
    path="/myroutepath"
    component={MyPageComponent}
    {...props}
  />
);

export default MyRoute;
```

5. Go to `/myroutepath` to see the rendered MyPageComponent.
