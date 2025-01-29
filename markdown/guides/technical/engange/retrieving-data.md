# Retrieving data from the store

This guide shows you how to retrieve data from the store after [fetching and processing the data](/guides/technical/engage/data-fetching-and-processing). Because the loyalty points we introduced in the [Loyalty Points Tutorial](/tutorials/kick-start/loyalty-points/frontend) are not part of the product data and have been stored in the Redux store, we now need to retrieve the data in order for our React component to re-render.

Retrieving data from the store is easy; the store is a plain javascript object. For smaller projects, you can use the native object path notation to access properties in the object. For more complex projects, like the applications in Shopgate Connect, it is best to use [Reselect](https://github.com/reduxjs/reselect). Reselect is a tool for optimizing Redux applications. It prevents unnecessary renders and improves performance for combining different pieces of the Redux state.

In order to access the loyalty points from our reducer, we need to write three functions that build upon each other. These functions live in `frontend/LoyaltyPoints/selectors.js`.

```javascript
import { createSelector } from 'reselect';

const getExtensionState = state =>
  state.extensions['@myAwesomeOrganization/loyalty-points'];

const getLoyaltyPointsState = createSelector(
  getExtensionState,
  extension => extension.loyaltyPoints
);

export const getLoyaltyPointsByProductId = createSelector(
  getLoyaltyPointsState
  (state, props) => props.productId,
  (loyaltyPointsState, productId) => {
    if (!productId) {
      return null;
    }

    const currentState = loyaltyPointsState[productId];

    if (!currentState || !currentState.points) {
      return null;
    }

    return loyaltyPointsState[productId].points;
  }
)
```

`getExtensionState` is a general selector that retrieves the state for your extension reducer. This state may hold other reducers as well and should not be connected to a React component directly. We use it to create another selector based off of it.

`getLoyaltyPointsState` retrieves our newly created loyalty points state. This is the basis for retrieving product-specific loyalty points and should also not be connected to a React component directly, since it holds data for multiple products. It uses the previous selector `getExtensionState` to retrieve the extension state and derive the loyalty points state from it.

`getLoyaltyPointsByProductId` is the actual selector we use to retrieve the loyalty points for a specific product. It uses the previous selector `getLoyaltyPointsState` to derive our loyalty points state for further selection. Notice that this is the only selector that is exported in the file because it is the only selector that we actually use when connecting the component.

> **NOTE**: The content of `frontend/LoyaltyPoints/selectors.js` is different from the Loyalty Points Tutorial. The selector from this document replaces the implementation from the Loyalty Points Tutorial.

Now we can start connecting the Redux store with our React component, with the help of our new selector.

## Connecting the store to the component

The Redux store and the React components are not directly connected. React bindings are not included in Redux by default. In order to achieve this, we use [React Redux](https://react-redux.js.org). React Redux provides the `connect` Higher Order Component (HOC) that allows React components to read data from the Redux store and dispatch actions to the store to update the data.

Now we change the implementation that already exists in `frontend/LoyaltyPoints/connector.js` from the [Loyalty Points Tutorial](/tutorials/kick-start/loyalty-points/frontend#creating-the-connector) to the following:

```javascript
import { connect } from 'react-redux';
// import { getProductLoyaltyPoints } from './selectors';
import { getLoyaltyPointsByProductId } from './selectors.js';

const mapStateToProps = (state, props) => ({
  // points: getProductLoyaltyPoints(state, props),
  points: getLoyaltyPointsByProductId(state, props),
});

export default connect(mapStateToProps);
```

**We import our newly created `getLoyaltyPointsByProductId` selector and use it instead of the one that was used in the [Loyalty Points Tutorial](/tutorials/kick-start/loyalty-points/frontend#creating-the-connector).**

> The commented out lines may be deleted. They are only shown in this example for clarification.

The `mapStateToProps` function is used by the `connect` HOC to pass the Redux state through the selectors and build new React component props. The returned object actually represents the component props.

We need to pass this function as the first argument of `connect`. The HOC then returns another function that we can use to inject the newly created props into the React component. You can see this inside the [Loyalty Points Tutorial](/tutorials/kick-start/loyalty-points/frontend).

**Now our component automatically receives the correct loyalty points when they are fetched, as seen in the guide on [fetching and processing data](/guides/technical/engage/data-fetching-and-processing)**
