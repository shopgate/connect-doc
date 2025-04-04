## What Are Streams?

Observable streams allow unrelated components, features, and extensions to interact with each other. You can filter Observable streams into multiple streams. Subscriptions can subscribe to these streams to perform tasks. Observable streams are based on the RxJS Library.

## How to Use Streams and Subscriptions

At Shopgate, the streams emit after a Redux action is fired. By default the `main$` stream fires for every action. Shopgate also provides a set of commonly used streams.
The following example illustrates how to filter the main$ stream, create a new stream, and create a subscription to the new stream.

**MyStream**

```js
import { main$ } from '@shopgate/engage/core;

// Create a new stream
export const loginSuccess$ = main$
  .filter(({ action }) => action.type === 'LOGIN_SUCCESS');
```

**MySubscriptionFile**

```js
import { loginSuccess$ } from 'MyExtensionPath/stream.js';

export default (subscribe) => {
  subscribe(loginSuccess$, ({ dispatch }) => {
    // Perform tasks after the user has logged in.
  });
};
```

## Adding Custom Streams and Subscriptions

You can add custom subscriptions from inside an extension to your theme. Create a custom subscription by adding a new entry into the `components` field of the `extension-config.json` file:

**extension-config.json**

```json
{
  ...
  "components": [
    ...
    {
      "id": "MyExtensionSubscription",
      "path": "<path>/<MySubscriptionFile>.js",
      "type": "subscribers"
    }
  ]
}
```
