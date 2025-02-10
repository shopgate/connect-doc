---
stoplight-id: fnhjakfiknpea
---

# Main Stream

## main$

This is the most basic stream that Shopgate provides. The main stream  triggers on _every_ redux action that is dispatched. You can derive your own streams from it.

> **CAUTION: Do not use this stream directly. The only purpose of the main stream is to derive further streams from it!**

### Usage

```javascript
import { main$ } from '@shopgate/engage/core';

const myCustomStream$ = main$.filter(({ action }) => action.type === 'MY_CUSTOM_ACTION_TYPE');
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { main$ } from '@shopgate/pwa-common/streams/main'`