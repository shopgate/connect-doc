---
stoplight-id: sh46jl9dt9qqf
---

# Router Actions

* [historyPush](#historypush)
* [historyPop](#historypop)
* [historyReplace](#historyreplace)
* [historyReset](#historyreset)

## historyPush

Triggers the browser history to PUSH a new page. This is a forward navigation.

### Usage

```javascript
import { historyPush } from '@shopgate/engage/core';

dispatch(historyPush({ pathname: '/' }));
```


### Parameters

* `params` *(Object)* __required__: The parameters for the PUSH action.
  * `pathname` *(string)* __required__: The pathname to navigate to.
  * `state` *(Object)*: With the state object data can be transfered to the upcoming route. The is NOT the redux state. It is metadata only for the routing transition.
  * `silent` *(boolean)*: Defaults to `false`. If this is set to `true`, redux will not react on the current routing action and not dispatch any further actions. This should only be used to prevent side effects!

---

## historyPop

Trigger the browset history to POP the current page. This is a backwards navigation.

### Usage

```javascript
import { historyPop } from '@shopgate/engage/core';

dispatch(historyPop());
```


---

## historyReplace

This will replace to current page with another. If no pathname to a new page is sent, it will POP the current page and therefore perform a backwards navigation instead.

### Usage

```javascript
import { historyReplace } from '@shopgate/engage/core';

dispatch(historyReplace({ pathname: '/some-page' }));
```



### Parameters

* `params` *(Object)* __required__: The parameters for the replace action.
  * `pathname` *(string)*: The pathname of the new page.
  * `state` *(Object)*: With the state object data can be transfered to the upcoming route. The is NOT the redux state. It is metadata only for the routing transition.
  * `silent` *(boolean)*: Defaults to `false`. If this is set to `true`, redux will not react on the current routing action and not dispatch any further actions. This should only be used to prevent side effects!

---

## historyReset

This will reset the browser history and clear the whole navigation stack.

### Usage

```javascript
import { historyReset } from '@shopgate/engage/core';

dispatch(historyReset());
```
