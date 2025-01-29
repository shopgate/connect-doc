---
title: Frontend Part
stoplight-id: fxpx2v4k0teui
---
# Tutorial - Loyalty Points Frontend

This tutorial shows you how to add a new Feature to the Product Detail Page of the Shopgate Engage app. This feature will display the user’s loyalty points that come in with the product data, as described in the [Backend Part](/tutorials/kick-start/loyalty-points/backend) of this tutorial.

This tutorial also shows you how to stylize the feature content using a tag symbol icon.

## Creating a React component

First, create the React component to display the points. Create a directory inside the extension frontend directory called `LoyaltyPoints`: `<extension-root>/frontend/LoyaltyPoints`. Inside this directory, create a new file called `index.jsx`.

Add the following code to the new file:

```jsx
import React from 'react';
import PropTypes from 'prop-types';

const LoyaltyPoints = ({ points }) => (
  points ? <div>Points: {points}</div> : null
);

LoyaltyPoints.propTypes = {
  points: PropTypes.number,
};

LoyaltyPoints.defaultProps = {
  points: 0,
};

export default LoyaltyPoints;
```

## Creating the icon

You need another component to render the icon. This component can then be imported and rendered by the LoyaltyPoints component.

Create a new directory next to the `LoyaltyPoints` directory called `LoyaltyIcon`. Then create an `index.jsx` file inside this new directory.

Add the following code to the new file:

```jsx
import React from 'react';
import { Icon } from '@shopgate/engage/components';

const content = '<path d="M23.292 11.5L12.492.7A2.384 2.384 0 0 0 10.8 0H2.4A2.407 2.407 0 0 0 0 2.4v8.4a2.4 2.4 0 0 0 .708 1.7l10.8 10.8a2.384 2.384 0 0 0 1.692.7 2.346 2.346 0 0 0 1.692-.708l8.4-8.4A2.346 2.346 0 0 0 24 13.2a2.424 2.424 0 0 0-.708-1.7zM4.2 6A1.8 1.8 0 1 1 6 4.2 1.8 1.8 0 0 1 4.2 6zm14.124 9.924L13.2 21.048l-5.124-5.124A3 3 0 0 1 10.2 10.8a2.964 2.964 0 0 1 2.124.888l.876.864.876-.876a3.004 3.004 0 1 1 4.248 4.248z" fill="none" stroke-linecap="round" stroke-linejoin="round"/>';

const LoyaltyIcon = props => (
  <Icon
    content={content}
    viewBox="-0.5 -0.5 25 25"
    {...props}
  />
);

export default LoyaltyIcon;
```

> **Note:**
>
> In the **Shopgate Engage** app, all icons are **SVG** to allow code splitting, support more icons, and to render faster and more effectively. For more details, refer to [why GitHub migrated](https://blog.github.com/2016-02-22-delivering-octicons-with-svg/) from font icons to SVG icons.

Now we can integrate this into our `LoyaltyPoints` component:

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import LoyaltyIcon from '../LoyaltyIcon';

const LoyaltyPoints = ({ points }) => (
  points ? (
    <div>
      <LoyaltyIcon />
      Points: {points}
    </div>
  ) : null
);

LoyaltyPoints.propTypes = {
  points: PropTypes.number,
};

LoyaltyPoints.defaultProps = {
  points: 0,
};

export default LoyaltyPoints;
```

## Styling the components

Now you can style the components. We recommend that you use the **glamor** package for styling. Refer to the **glamor** [documentation](https://github.com/threepointone/glamor#glamor) for more information.

> For more details on how to apply styling in **Shopgate Engage**, refer to the Shopgate  guide about [styling components](/guides/technical/engage/styling-components).

Create a new file called `style.js` inside the `LoyaltyPoints` component directory with the following content:

```jsx
import { css } from 'glamor';
import { themeConfig } from '@shopgate/engage';

const container = css({
  alignItems: 'center',
  display: 'flex',
  fontSize: 14,
  marginTop: 16,
});

const icon = css({
  height: 24,
  marginRight: 4,
  stroke: themeConfig.colors.accent,
  width: 24,
});

export default {
  container,
  icon,
};
```

Now you can apply those styles to the `LoyaltyPoints` component.

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import LoyaltyIcon from '../LoyaltyIcon';
import styles from './style';

const LoyaltyPoints = ({ points }) => (
  points ? (
    <div className={styles.container}>
      <LoyaltyIcon className={styles.icon} />
      Points: {points}
    </div>
  ) : null
);

LoyaltyPoints.propTypes = {
  points: PropTypes.number,
};

LoyaltyPoints.defaultProps = {
  points: 0,
};

export default LoyaltyPoints;
```

## Adding custom translations

Now, add the strings you want to use. The strings to add in this example are `Points` (English) and `Punkte` (German).

Since the loyalty points are shown on the product page, we should add the strings to the product key in the locale file. This process has to be repeated for each file.

To add the new strings, create a file for each language in the `<extension-root>/frontend` directory. Name the files `en-US.json` and `de-DE.json`. The contents of these files merges with the theme locale file.

The locale files should look like this:

### en-US.json

```json
{
  "product": {
    "loyalty": "Points"
  }
}
```

### de-DE.json

```json
{
  "product": {
    "loyalty": "Punkte"
  }
}
```

Now, update the `LoyaltyPoints` component to use the translation component from the Shopgate library.

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import { I18n } from '@shopgate/engage/components';
import LoyaltyIcon from '../LoyaltyIcon';
import styles from './style';

const LoyaltyPoints = ({ points }) => (
  points ? (
    <div className={styles.container}>
      <LoyaltyIcon className={styles.icon} />
      <I18n.Text string="product.loyalty" />: {points}
    </div>
  ) : null
);

LoyaltyPoints.propTypes = {
  points: PropTypes.number,
};

LoyaltyPoints.defaultProps = {
  points: 0,
};

export default LoyaltyPoints;
```

## Connecting to the Product Data

You now have a working component. However, the amount of loyalty points that is shown is static. We need to connect the component to the Redux store to display the correct amount for each product.

To do this we need to:

* Create a selector to get the data from the store.
* Create a connector to map the data to the component props.
* Adjust the component to use the connector.

### Creating the selector

Selectors are an efficient way to retrieve data from the store. You can read more about selectors in the Reselect [documentation](https://github.com/reduxjs/reselect#reselect).

The selector returns the value of the `loyaltyPoints` field from the current product. If there is no value present, the value defaults to null.

> It is good practice to create selectors that return a predictable value when data is unavailable.

Next, create a new file called `selectors.js` inside the `LoyaltyPoints` directory with the following content:

```js
import { createSelector } from 'reselect';
import { getProduct } from '@shopgate/engage/product';

export const getProductLoyaltyPoints = createSelector(
  getProduct,
  product => product ? product.loyaltyPoints : null
);
```

### Creating the connector

A connector is a Higher Order Component that injects props from a redux store into a component. You can read more about connectors in the Redux [documentation](https://redux.js.org/basics/usage-with-react).

Create a new file inside the `LoyaltyPoints` directory called `connector.js`.

Now you can use the previously created selector to inject the correct amount of loyalty points into the `points` prop of the `LoyaltyPoints` component:

```js
import { connect } from 'react-redux';
import { getProductLoyaltyPoints } from './selectors';

const mapStateToProps = (state, props) => ({
  points: getProductLoyaltyPoints(state, props),
});

export default connect(mapStateToProps);
```

> Notice that we need to pass the component props into the selector as well. The props hold the `productId` that retrieves the correct set of loyalty points data.

### Connect the component

Now, adjust the `LoyaltyPoints` component to use the connector.

To do this, we need to import the connector and the Theme API component in order to match the component to the current product data and then create an additional container component that maps that to the new connector:

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import { I18n } from '@shopgate/engage/components';
import { Theme } from '@shopgate/engage/core';
import LoyaltyIcon from '../LoyaltyIcon';
import styles from './style';
import connect from './connector';

const LoyaltyPoints = ({ points }) => (
  points ? (
    <div className={styles.container}>
      <LoyaltyIcon className={styles.icon} />
      <I18n.Text string="product.loyalty" />: {points}
    </div>
  ) : null
);

LoyaltyPoints.propTypes = {
  points: PropTypes.number,
};

LoyaltyPoints.defaultProps = {
  points: 0,
};

// Connect your component to the store.
const LoyaltyPointsConnected = connect(LoyaltyPoints);

// Tell the connected component what product page you are on.
export default () => (
  <Theme>
    {({ contexts: { ProductContext } }) => (
      <ProductContext.Consumer>
        {productProps => <LoyaltyPointsConnected {...productProps} />}
      </ProductContext.Consumer>
    )}
  </Theme>
);
```

## Integrating with the theme

The final step is to add the new component to the product page. To do this, we need to add some entries to the `components` field. This field is inside the `extension-config`, at the root of the extension. The target of the `LoyaltyPoints` component is `product.availability.after`. This instructs the theme to display the component at the `PRODUCT_AVAILABILITY_AFTER` portal position.

```json
{
  ...
  "components": [
    {
      "id": "LoyaltyPoints",
      "path": "frontend/LoyaltyPoints/index.jsx",
      "target": "product.availability.after",
      "type": "portals"
    },
    {
      "id": "en-US",
      "path": "frontend/en-US.json",
      "type": "translations"
    },
    {
      "id": "de-DE",
      "path": "frontend/de-DE.json",
      "type": "translations"
    }
  ]
  …
}
```
