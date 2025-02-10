---
stoplight-id: yzxyam3a4yfdd
---

# User Streams

* [userWillLogin$](#userwilllogin)
* [userLoginResponse$](#userloginresponse)
* [userDidLogin$](#userdidlogin)
* [userWillLogout$](#userwilllogout)
* [userDidLogout$](#userdidlogout)
* [userDidUpdate$](#userdidupdate)
* [userDataReceived$](#userdatareceived)
* [loginDidFail$](#logindidfail)

## userWillLogin$

Triggers when a user submits the login form.

### Usage

```javascript
import { userWillLogin$ } from '@shopgate/engage/user';

subscribe(userWillLogin$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userWillLogin$ } from '@shopgate/pwa-common/streams/user'`

---

## userLoginResponse$

Triggers when the login request receives a response.

### Usage

```javascript
import { userLoginResponse$ } from '@shopgate/engage/user';

subscribe(userLoginResponse$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userLoginResponse$ } from '@shopgate/pwa-common/streams/user'`

---

## userDidLogin$

Triggers when the user logged in.

### Usage

```javascript
import { userDidLogin$ } from '@shopgate/engage/user';

subscribe(userDidLogin$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userDidLogin$ } from '@shopgate/pwa-common/streams/user'`

---

## userWillLogout$

Triggers when the user requests the logout action.

### Usage

```javascript
import { userWillLogout$ } from '@shopgate/engage/user';

subscribe(userWillLogout$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userWillLogout$ } from '@shopgate/pwa-common/streams/user'`

---

## userDidLogout$

Triggers when the user logged out.

### Usage

```javascript
import { userDidLogout$ } from '@shopgate/engage/user';

subscribe(userDidLogout$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userDidLogout$ } from '@shopgate/pwa-common/streams/user'`

---

## userDidUpdate$

Triggers when the user data changes.

### Usage

```javascript
import { userDidUpdate$ } from '@shopgate/engage/user';

subscribe(userDidUpdate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userDidUpdate$ } from '@shopgate/pwa-common/streams/user'`

---

## userDataReceived$

Triggers when user data is received from the server.

### Usage

```javascript
import { userDataReceived$ } from '@shopgate/engage/user';

subscribe(userDataReceived$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { userDataReceived$ } from '@shopgate/pwa-common/streams/user'`

---

## loginDidFail$

Triggerswhen the login process fails.

### Usage

```javascript
import { loginDidFail$ } from '@shopgate/engage/user';

subscribe(loginDidFail$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { loginDidFail$ } from '@shopgate/pwa-common/streams/user'`