# Fetching and Processing Data

This guide builds on the [Loyalty Points Tutorial](/tutorials/kick-start/loyalty-points/frontend). But unlike in the frontend tutorial, we assume that the points are not available within the product state. Instead, we maintain the points per product within a custom Redux state and fetch them via a PipelineRequest or an AJAX request.

## Preparing to Enable Data Persistence with Redux

Since the loyalty points for a product are static values, it is not necessary to request them again when a product is reopened. Therefore, we can put them into the Redux store, like the product data itself. When the `LoyaltyPoints` component is rendered, it first tries to grab the required data from the store, before fetching it from the backend.

Before we return to the component itself, we must implement some `actions` that are the foundation of the communication with Redux. According to the [Redux documentation](https://redux.js.org/basics/actions)

> Actions are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using `store.dispatch()`.

### Creating Action Creators

Since actions transfer dynamic data to the store, they need to be constructed on demand. Therefore, we use `action creators` located within `frontend/action-creators.js`.

```javascript
export const REQUEST_LOYALTY_POINTS = 'REQUEST_LOYALTY_POINTS';

export const requestLoyaltyPoints = productId => ({
  type: REQUEST_LOYALTY_POINTS,
  productId,
});
```

The `requestLoyaltyPoints` action is dispatched to Redux right before the data request is dispatched. The updated data within the related store entry could be used to render the connected React components with a loading indicator.

```javascript
export const RECEIVE_LOYALTY_POINTS = 'RECEIVE_LOYALTY_POINTS';

export const receiveLoyaltyPoints = (productId, points) => ({
  type: RECEIVE_LOYALTY_POINTS,
  productId,
  points,
});
```

After the response is received, the `receiveLoyaltyPoints` action is dispatched to put the points into the store.

```javascript
export const ERROR_LOYALTY_POINTS = 'ERROR_LOYALTY_POINTS';

export const errorLoyaltyPoints = (productId) => ({
  type: ERROR_LOYALTY_POINTS,
  productId,
});
```

When a response is erroneous, the `errorLoyaltyPoints` action dispatches to reset the related store entry, so that connected React components can update their presentation.

### Creating Async Actions

After adding actions that can be used to add or update data within the Redux store, you must define the logic that retrieves the loyalty points from the backend. The previous actions just returned a simple object, but it is also possible to return a function that can contain asynchronous logic - a [Redux Thunk](https://github.com/reduxjs/redux-thunk).

This function is invoked with a `dispatch` function, which allows you to dispatch other Redux actions. These actions can return values, like Promises. Therefore, you can implement additional handling from the outside.

In the next example, we'll use a Pipeline request to fetch the data. Alternatively, we could also use the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to retrieve data. The pipeline is called `myAwesomeOrganization.catalog.loyaltyPoints`. Loyalty points are assigned to products, so the Pipeline needs a single `input` parameter, which is called `productId`.

Our code is located within `frontend/actions.js`.

```javascript
import { PipelineRequest } from '@shopgate/engage/core';
import {
  requestLoyaltyPoints,
  receiveLoyaltyPoints,
  errorLoyaltyPoints,
} from './action-creators';

const fetchLoyaltyPoints = productId => dispatch => {

  dispatch(requestLoyaltyPoints(productId));

  return new PipelineRequest('myAwesomeOrganization.catalog.loyaltyPoints')
    .setInput({ productId })
    .dispatch()
    .then(points => dispatch(receiveLoyaltyPoints(productId, points))
    .catch(error => {
      // Implement your desired error handling.
      dispatch(errorLoyaltyPoints(productId));
    });
};

export default fetchLoyaltyPoints;
```

### Creating a Reducer

We have now created regular actions and dispatched them within an asynchronous action. You might be wondering how the data that we sent with the actions eventually reaches the store. That is when `reducers` come into play.

Reducers create a new state within the Redux store, and maintain it based on the action `type` and its payload. To explore this topic more deeply, consult the related [Redux documentation](https://redux.js.org/basics/reducers).

To register a new reducer at Redux, we need to add a new entry into the components list of you `extension-config.json`.

```json
{
  ...
  "id": "@myAwesomeOrganization/loyalty-points"
  "components": [
    ...
    {
      "id": "loyaltyPoints",
      "path": "frontend/reducer.js",
      "type": "reducers"
    },
  ]
}
```

This adds a new state to Redux which is accessible within `state.extensions['@myAwesomeOrganization/loyalty-points'].loyaltyPoints`. For our example, we put the related code into `frontend/reducer.js`.

```javascript
import {
  REQUEST_LOYALTY_POINTS,
  RECEIVE_LOYALTY_POINTS,
  ERROR_LOYALTY_POINTS,
} from './action-creators';

export default function loyaltyPoints(state = {}, action) {
  switch(action.type) {
    case REQUEST_LOYALTY_POINTS:
      return {
        ...state,
        [action.productId]: {
          ...state[action.productId],
          isFetching: true,
          expires: 0,
        },
      };
    case RECEIVE_LOYALTY_POINTS:
      return {
        ...state,
        [action.productId]: {
          ...state[action.productId],
          points: action.points,
          isFetching: false,
          expires: Date.now() + 3600,
        },
      };
    case ERROR_LOYALTY_POINTS:
      return {
        ...state,
        [action.productId]: {
          ...state[action.productId],
          isFetching: false,
        },
      };
    default:
      return state;
  }
};
```

You may recognize all `types` from the actions we created at the beginning of this guide.

`REQUEST_LOYALTY_POINTS` adds a new entry to the state, which is referenced by the `productId` from the action payload. The entry indicates that a request is currently ongoing. Additionally, it contains an `expires` flag, which we can later use to determine if the stored state is still valid or if new data needs to be requested.

`RECEIVE_LOYALTY_POINTS` updates the state entry with the loyalty points from the request response, resets the `isFetching` flag, and applies an expiration date to the entry.

`ERROR_LOYALTY_POINTS` resets the `isFetching` flag so that when you design your asynchronous action so that requests are not dispatched when identical requests are already ongoing, you can unblock this logic to enable retries.

## Data Fetching

This section focuses on two general approaches to facilitate data fetching. The first one uses a [stream subscription](/guides/technical/engage/streams) to fetch the required data. Besides the connector changes from above, the component does not need to be touched.

Alternatively, we can inject a function into the props of the `LoyaltyPoints` component which can be called within a React lifecycle hook. Since this might interfere with some React best practices, the first approach is preferred. However, depending on the use case, this approach might not be an option.

### Creating a Subscription

Fetching data within a subscription is quite easy. We just need to subscribe to a suitable stream. The Engage libraries offer a broad variety of pre-configured streams. For an overview, please consult our [references](https://developer.shopgate.com/references/engage/streams).

Subscriptions need to be registered via the `extension-config.json` and could look like this:

```json
{
  ...
  "components": [
    ...
    {
      "id": "LoyaltyPointsSubscriptions",
      "path": "frontend/subscriptions.js",
      "type": "subscribers"
    },
  ]
}
```

For our example, we use the [`productWillEnter$`](https://developer.shopgate.com/references/engage/streams/product#productwillenter) stream which emits when a product is about to be opened. So whenever a user opens a Product Detail Page, the points are requested. Our `LoyaltyPoints` component re-renders automatically after the points from the response are added to the Redux store.

```javascript
import { hex2bin } from '@shopgate/engage/core';
import { productWillEnter$ } from '@shopgate/engage/product';
import { getLoyaltyPointsByProductId } from './selectors';
import { fetchLoyaltyPoints } from './actions';

export default function loyaltyPoints(subscribe) {
  subscribe(productWillEnter$, ({ action dispatch }) => {
    /**
     * Get the productId from the route params. Since these ids are potentially not URL safe, the
     * URLs contain a bin2hex encrypted version. We need to decrypt them before we can use them.
     */
    const { productId } = action.route.params;
    const id = hex2bin(productId);

    dispatch(fetchLoyaltyPoints(id));
  });
}

```

### Fetching within a Component Lifecycle Hook

In this section, we refactor our `LoyaltyPoints` a little bit, so that we can dispatch the loyalty points request from within a React component lifecycle hook. The `connect` HOC of React Redux allows you to pass a second argument called `mapDispatchToProps`. Like `mapStateToProps` it can be used to inject extra props to a component.

#### Extending the Connector

After the adjustments, our file at `frontend/LoyaltyPoints/connector.js` looks like this.

```javascript
import { connect } from 'react-redux';
import { fetchLoyaltyPoints } from '../actions';

const mapStateToProps = (state, props) => ({
  ...
});

const mapDispatchToProps = (dispatch, props) =>({
  fetchPoints: () => dispatch(fetchLoyaltyPoints(props.productId)),
});

export default connect(mapStateToProps, mapDispatchToProps);
```

The extended connector adds an additional prop called `fetchPoints` to the component. When invoked, it dispatches the `fetchLoyaltyPoints` action to Redux, which fetches the points for the passed `productId`. After a response is received, the Redux state updates, which results in re-rendering the component with the received points.

#### Updating the Component

The final step is to invoke the function within our component. The component from the tutorial is implemented as a functional component that does not have lifecycle hooks. So we need to transform it into a real component now. Once this step is complete, our component is successfully connected to our custom Redux state.

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import { I18n } from '@shopgate/engage/components';
import LoyaltyIcon from '../LoyaltyIcon';
import styles from './style';

class LoyaltyPoints extends Component {
  static propTypes = {
    fetchPoints: PropTypes.func.isRequired,
    points: PropTypes.number,
  }

  static defaultProps = {
    points: null,
  }

  static getDerivedStateFromProps(nextProps) {
    // Fetch the points, when no valid store entry is available yet.
    if (nextProps.points === null) {
      nextProps.fetchPoints();
    }

    return null;
  }

  render() {
    const { points } = this.props;

    if (!points) {
      return null;
    }

    return (
      <div className={styles.container}>
        <LoyaltyIcon className={styles.icon} />
        <I18n.Text string="product.loyalty" />: {points}
      </div>
    )
  }
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
