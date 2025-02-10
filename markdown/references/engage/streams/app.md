---
stoplight-id: lf7wsjtipjzy8
---

# App Streams

* [appWillStart$](#appwillstart)
* [appDidStart$](#appdidstart)

## appWillStart$

Triggers immediately before the application starts. At this moment, the redux store is already initiated, but React has not started rendering.

### Usage

```javascript
import { appWillStart$ } from '@shopgate/engage/core';

subscribe(appWillStart$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { appWillStart$ } from '@shopgate/pwa-common/streams/app'`

---

## appDidStart$

Triggers when the main `<App />` component is mounted to the DOM.

### Usage

```javascript
import { appDidStart$ } from '@shopgate/engage/core';

subscribe(appDidStart$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { appDidStart$ } from '@shopgate/pwa-common/streams/app'`