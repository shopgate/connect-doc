---
stoplight-id: f8wpmspxnmtly
---

# HOCs

Shopgate ENGAGE provides [Higher Order Components](https://reactjs.org/docs/higher-order-components.html) (HOCs) to make it easier for you to access features and information while developing your React components:

* [withTheme](#withtheme)
* [withRoute](#withroute)
* [withCurrentProduct](#withcurrentproduct)
* [withNavigation](#withnavigation)

---

## withTheme

Passes the Theme API components directly into your React component.

### Usage

```javascript
import { withTheme } from '@shopgate/engage/core';

function MyReactComponent({ View, AppBar }) {
  return (
    // your component output goes here.
  )
}

export default withTheme(MyReactComponent);
```

### Adds

The theme API containing theme specific styled React components.

> You can find more detailed information about the components in the [Theme API documentation](/references/engage/theme).

---

## withRoute

Passes contextual information about the current route into your React component.

### Usage

```javascript
import { withRoute } from '@shopgate/engage/core';

function MyReactComponent({ pathname, visible }) {
  if (pathname !== '/some-route' || !visible) {
    return null;
  }

  return (
    // You component output goes here.
  );
}

export default withRoute(MyReactComponent);
```

In this example you can see how you can get information about the current **pathname** and the **visibility** of the current route. This can be used to control the render output of your component and is especially helpful for creating a **Custom Route**.

### Adds

The route context information:

| Name     | Type      | Description                                                     |
| -------- | --------- | --------------------------------------------------------------- |
| visible  | _boolean_ | Whether the route is visible in the app.                        |
| pathname | _string_  | The current route's pathname.                                   |
| location | _string_  | The full history location of the current route.                 |
| params   | _Object_  | The route parameters that are specified in the route's pattern. |
| query    | _Object_  | The GET parameters.                                             |
| state    | _Object_  | Custom data that can be passed to a route on when navigating.   |

---

## withCurrentProduct

Passes information about the currently viewed Product on a Product Detail Page to your React Component.

### Usage

```javascript
import { withCurrentProduct } from '@shopgate/engage/core';

function MyReactComponent({ productId, variantId }) {
  return (
    // You component output goes here.
  );
}

export default withCurrentProduct(MyReactComponent);
```

### Adds

The product information:

| Name          | Type          | Description                                                                                                                                                                                         |
| ------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| productId     | _string_      | The product ID.                                                                                                                                                                                     |
| variantId     | _string_      | The product ID of a variant if the current product is a selected variant.                                                                                                                           |
| options       | _Object_      | The selected product options.                                                                                                                                                                       |
| optionsPrices | _Object_      | The price values of the selected product options.                                                                                                                                                   |
| currency      | _string_      | The currency code of the product.                                                                                                                                                                   |
| conditioner   | _Conditioner_ | Helps you control the dependencies between multiple possible variant selections. This also controls if a product can only be added to the cart if a specific type of variant has been selected. |

## withNavigation

Passes helper functions for easy navigation into your React Component.

### Usage

```javascript
import { withNavigation } from '@shopgate/engage/core';

function MyReactComponent({ historyPush }) {
  return (
    <button onClick={() => historyPush({ pathname: '/some-link' })}>Click Me</button>
  );
}

export default withNavigation(MyReactComponent);
```

### Adds

The navigation helper functions:

| Name             | Parameters                                                                                                                                 | Description                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| `historyPush`    | Receives the same arguments as the redux action.                                                                                           | Performs the [historyPush](/references/engage/actions/router#historypush) navigation action.       |
| `historyPop`     | -                                                                                                                                          | Performs the [historyPop](/references/engage/actions/router#historypop) navigation action.         |
| `historyReplace` | Receives the same arguments as the redux action.                                                                                           | Performs the [historyReplace](/references/engage/actions/router#historyreplace) navigation action. |
| `historyReset`   | -                                                                                                                                          | Performs the [historyReset](/references/engage/actions/router#historyreset) navigation action.     |
| `historyUpdate`  | - `state` *(Object)* __required__: The state to be updated on the desired Route.<br>- `routeId` *(string)*: The ID of the route to update. | Updates a certain (usually the current) route's meta state object with new data.                   |