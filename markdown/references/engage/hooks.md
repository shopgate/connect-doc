---
stoplight-id: fiswddb89tznw
---

# Hooks

Shopgate Engage provides [React Hooks](https://reactjs.org/docs/hooks-intro.html) to make it easier for you to access features and information while developing your React components:

* [useTheme](#usetheme)
* [useRoute](#useroute)
* [useCurrentProduct](#usecurrentproduct)
* [useNavigation](#usenavigation)

---

## useTheme

Retrieves the Theme API components directly in your React component.

### Usage

```javascript
import { useTheme } from '@shopgate/engage/core';

function MyReactComponent() {
  const { View, AppBar } = useTheme();

  return (
    // your component output goes here.
  )
}
```

### Returns

*(Object)* - The theme API containing theme specific, styled React components.

> You can find more detailed information about the components in the [Theme API documentation](theme/overview.md).

---

## useRoute

Retrieves contextual information about the current route.

### Usage

```javascript
import { useRoute } from '@shopgate/engage/core';

function MyReactComponent() {
  const { pathname, visible } = useRoute();

  if (pathname !== '/some-route' || !visible) {
    return null;
  }

  return (
    // Your component output goes here.
  );
}
```

This example demonstrates how to get information about the current **pathname** and the **visibility** of the current route. This information can be used to control the render output of your component and is especially helpful for creating a **Custom Route**. You can find detailed instructions on [Creating Custom Routes](../../guides/technical/engage/creating-custom-routes.md) in the Shopgate Guides section.

### Returns

*(Object)* - The route context information:

| Name     | Type      | Description                                                     |
| -------- | --------- | --------------------------------------------------------------- |
| visible  | _boolean_ | Indicates if the route is visible in the app.                   |
| pathname | _string_  | The current route's pathname.                                   |
| location | _string_  | The full history location of the current route.                 |
| params   | _Object_  | The route parameters that are specified in the route's pattern. |
| query    | _Object_  | The GET parameters.                                             |
| state    | _Object_  | Custom data that can be passed to a route when navigating.      |

---

## useCurrentProduct

Retrieves information about the currently viewed Product on a Product Detail Page.

### Usage

```javascript
import { useCurrentProduct } from '@shopgate/engage/core';

function MyReactComponent() {
  const { productId, variantId } = useCurrentProduct();

  return (
    // You component output goes here.
  );
}
```

### Returns

*(Object)*  The product information:

| Name          | Type          | Description                                                                                                                                                                              |
| ------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| productId     | _string_      | The product ID.                                                                                                                                                                          |
| variantId     | _string_      | The product ID of a variant if the current product is a selected variant.                                                                                                                |
| options       | _Object_      | The selected product options.                                                                                                                                                            |
| optionsPrices | _Object_      | The price values of the selected product options.                                                                                                                                        |
| currency      | _string_      | The currency code of the product.                                                                                                                                                        |
| conditioner   | _Conditioner_ | Helps to control the dependencies between multiple possible variant selections. This also controls if a product can only be added to the cart if a specific type of variant is selected. |

## useNavigation

Provides helper functions for easy navigation through the application.

### Usage

```javascript
import { useNavigation } from '@shopgate/engage/core';

function MyReactComponent() {
  const { push } = useNavigation();

  return (
    <button onClick={() => push({ pathname: '/some-link' })}>Click Me</button>
  )
}
```

### Returns

*(Object)* An object containing navigation helpers:

| Name      | Parameters                                                                                                                                 | Description                                                                                        |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| `push`    | Receives the same arguments as the redux action.                                                                                           | Performs the [historyPush](actions/router.md#historypush) navigation action.       |
| `pop`     | -                                                                                                                                          | Performs the [historyPop](actions/router.md#historypop) navigation action.         |
| `replace` | Receives the same arguments as the redux action.                                                                                           | Performs the [historyReplace](actions/router.md#historyreplace) navigation action. |
| `reset`   | -                                                                                                                                          | Performs the [historyReset](actions/router.md#historyreset) navigation action.     |
| `update`  | - `state` *(Object)* __required__: The state to be updated on the desired Route.<br>- `routeId` *(string)*: The ID of the route to update. | Updates a certain (usually the current) route's meta state object with new data.                   |

## useReduceMotion

Provides accessibility information in case user has activated "reduce motion" on the device.

### Usage

```javascript
import { useReduceMotion } from '@shopgate/engage/a11y/hooks';
const reduceMotion = useReduceMotion();
```
### Example

```html
<video src={url} autoPlay={reduceMotion ? false : autoplay}> </video>
```