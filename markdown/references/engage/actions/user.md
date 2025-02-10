---
stoplight-id: 6yo0zwtb3lo0s
---

# User Actions

* [fetchRegisterUrl](#fetchregisterurl)
* [fetchUser](#fetchuser)
* [login](#login)
* [logout](#logout)

## fetchRegisterUrl

Fetches the URL for user registration.

### Usage

```js
import { fetchRegisterUrl } from '@shopgate/engage/user';

dispatch(fetchRegisterUrl());
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import fetchRegisterUrl from '@shopgate/pwa-common/actions/user/fetchRegisterUrl'`

---

## fetchUser

Fetches the data of the current user.

### Usage

```js
import { fetchUser } from '@shopgate/engage/user';

dispatch(fetchUser());
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import fetchUser from '@shopgate/pwa-common/actions/user/fetchUser'`

---

## login

Log in a user.

### Usage

```js
import { login } from '@shopgate/engage/user';

dispatch(login({login: 'user@email.com', password: 'password123'}, '/checkout', 'basic'));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import login from '@shopgate/pwa-common/actions/user/login'`

### Parameters

* `parameters` *(Object)*:  The login credentials.
  * `login` *(string)*: The username.
  * `password` *(string)*: The password.
* `redirect` *(string)* : The location to direct the user after login.
* `strategy` *(string)*  Login method, such as ‘basic’, ‘facebook’, or ‘amazon’.

---

## logout

Log out the current user.

### Usage

```js
import { logout } from '@shopgate/engage/user';

dispatch(logout());
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import logout from '@shopgate/pwa-common/actions/user/logout'`