# Creating Custom Routes

You can create new pages for your extensions using custom routes. Follow these steps to add a new page to [__Shopgate Engage__](https://www.shopgate.com/en/solutions/engage-mobile-app/).

First, create the components inside your extension.

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';

function MyPage() {
  return (
    <div>Hello World!</div>
  );
}

export default () => (
  <Route pattern="/myroute" component={MyRoute} />
);
```

> When working with __Engage v6.1__ and above, it is possible to put all route exports into a single file enclosed by a `<Fragment>`. Here is an example:

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

> To add multiple routes in __Engage__ versions below __6.1__, you must put each route into its own file or directly into the page component. Then, you can add all route export files.

## Using existing theme components

Shopgate offers some components to help you bootstrap your page for consistency.  You can access these components through the `Theme` Provider component in the `@shopgate/pwa-common` library.

> **Note:**
>
> This example includes the `<AppBar>` component. The `<AppBar>` component is only available in this context as of __Engage 6.1__.

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

__Engage v6.5__ introduces support for React Hooks. These hooks provide access to the theme components inside your Custom Route's page component, thereby reducing component overhead.

```jsx
import React from 'react';
import { Route } from '@shopgate/engage/components';
import { useTheme } from '@shopgate/engage/core';

function MyPage() {
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
