# Creating Custom Routes

You can create new pages for your extensions using custom routes. Follow these steps to add a new page to you app.

First, create the components inside your extension.

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';

function MyRoute() {
  return (
    <div>Hello World!</div>
  );
}

export default () => (
  <Route pattern="/myroute" component={MyRoute} />
);
```

> It is possible to put all route exports into a single file enclosed by a `<Fragment>`. Here is an example:

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';
import MyFirstPage from './pages/MyFirstPage';
import MySecondPage from './pages/MySecondPage';

export default () => (
  <Fragment>
    <Route pattern="/myfirstpage" component={MyFirstPage} />
    <Route pattern="/mysecondpage" component={MySecondPage} />
  </Fragment>
);
```

Then adjust the `extension-config.json` to inject the new page into the theme.

```json
{
  components: [
    {
      "id": "MyPage",
      "path": "<relative-path-to-the-component>",
      "target": "app.routes",
      "type": "portals"
    },
  ]
}
```

This code creates a page that you access through the `/myroute` pathname and renders some text onto a blank page.

## Using existing theme components

Shopgate offers some components to help you bootstrap your page for consistency.  You can access these components through the `Theme` Provider component in the `@shopgate/pwa-common` library.

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';
import { Theme } from '@shopgate/engage/core';

function MyPage() {
  return (
    <Theme>
      {({ View, AppBar }) => (
        <View>
          <AppBar title="MyRoute" />
          <div>Hello World!</div>
        </View>
      )}
    </Theme>
  );
}

export default () => (
  <Route pattern="/myroute" component={MyRoute} />
);
```

## Using React Hooks

React Hooks provide access to the theme components inside your Custom Route's page component, thereby reducing component overhead.

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';
import { useTheme } from '@shopgate/engage/core';

function MyRoute() {
  const { View, AppBar } = useTheme();

  return (
    <View>
      <AppBar title="MyRoute" />
      <div>Hello World!</div>
    </View>
  );
}

export default () => (
  <Route pattern="/myroute" component={MyRoute} />
);
```
