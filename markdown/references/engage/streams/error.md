---
stoplight-id: ln4i6vcqq30m7
---

# Error Streams

* [appError$](#apperror)
* [pipelineError$](#pipelineerror)

## appError$

Triggers when a JavaScript error occurs within the application.

### Usage

```javascript
import { appError$ } from '@shopgate/engage/core';

subscribe(appError$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { appError$ } from '@shopgate/pwa-common/streams/error'`

---

## pipelineError$

Triggers when a pipeline throws an error.

### Usage

```javascript
import { pipelineError$ } from '@shopgate/engage/core';

subscribe(pipelineError$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { pipelineError$ } from '@shopgate/pwa-common/streams/error'`