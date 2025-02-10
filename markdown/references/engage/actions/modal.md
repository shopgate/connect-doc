---
stoplight-id: yvuplxmf961fx
---

# Modal Actions

* [showModal](#showmodal)
* [closeModal](#closemodal)

## showModal

Shows a modal and returns a Promise that resolves when the modal closes. Depending on the user decision, the Promise resolves with `true` _(confirmed)_ or `false` _(dismissed)_.

### Usage

```js
import { showModal } from '@shopgate/engage/core';

dispatch(showModal({
  confirm: null,
  title: 'Modal title',
  message: 'modal.message',
  params: {
    param: 'Modal Param',
  }
}));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import showModal from '@shopgate/pwa-common/actions/modal/showModal'`

### Parameters

* `options` *(Object)* __required__: Options used by the modal.
  * `title` *(string)* __required__: The title for the modal (i18n placeholder support from v6.5.0).
  * `message` *(string)* : The message for the modal (i18n placeholder support from v6.7.0).
  * `confirm` *(string)*: The confirmation button label.
  * `dismiss` *(string)*: The dismiss button label.
  * `params` *(Object)*: Extra parameters for i18n placeholders.

---

## closeModal

Closes an open modal and resolves the mapped Promise.

### Usage

```js
import { closeModal } from '@shopgate/engage/core';

dispatch(closeModal(123, true))
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import closeModal from '@shopgate/pwa-common/actions/modal/closeModal'`

### Parameters

* `id` *(number)*: The ID of the modal to close.
* `confirmed` *(boolean)*: Whether the modal is confirmed or not.