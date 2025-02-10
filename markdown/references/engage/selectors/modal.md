---
stoplight-id: cd6iv6cdp6g8k
---

# Modal Selectors

* [getFirstModal](#getfirstmodal)
* [getModalById](#getmodalbyid)

## getFirstModal

Retrieves the first modal off the stack from the modal data in the store.

### Usage

```javascript
import { getFirstModal } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFirstModal } from '@shopgate/pwa-common/selectors/modal'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(Object|undefined)_: The modal information for the first item in the stack. If no modal information is found, it returns `undefined`.

---

## getModalById

Retrieves the modal information for a modal ID from the modal data in the store.

### Usage

```javascript
import { getModalById } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getModalById } from '@shopgate/pwa-common/selectors/modal'`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `modalId` _(string)_ **required**: The modal ID to look for.

### Returns

_(Object|undefined)_: The modal information by ID. If no modal information is found, it returns `undefined`.