## What Are Streams?

Observable streams allow unrelated components, features, and extensions to interact with each other. You can filter Observable streams into multiple streams. Subscriptions can subscribe to these streams to perform tasks. Observable streams are based on the RxJS Library. Refer to the [RxJS documentation](https://www.learnrxjs.io/) for more information.
An Observable is similar to an event emitter. When a condition is met, Observables emit a stream  that is available for subscription. You can also apply operators to Observables to create and control more complex scenarios for when a stream emits. By default, Shopgate imports the following operators:

* [do](https://www.learnrxjs.io/operators/utility/do.html)
* [distinctUntilChanged](https://www.learnrxjs.io/operators/filtering/distinctuntilchanged.html)
* [filter](https://www.learnrxjs.io/operators/filtering/filter.html)
* [first](https://www.learnrxjs.io/operators/filtering/first.html)
* [map](https://www.learnrxjs.io/operators/transformation/map.html)
* [merge](https://www.learnrxjs.io/operators/combination/merge.html)
* [shareReplay](https://www.learnrxjs.io/operators/multicasting/sharereplay.html)
* [switchMap](https://www.learnrxjs.io/operators/transformation/switchmap.html)
* [zip](https://www.learnrxjs.io/operators/combination/zip.html)

For a complete list of operators and examples, refer to [RxJS 5 Operators By Example](https://www.learnrxjs.io/operators/).

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
