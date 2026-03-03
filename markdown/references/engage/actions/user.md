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

---

## fetchUser

Fetches the data of the current user.

### Usage

```js
import { fetchUser } from '@shopgate/engage/user';

dispatch(fetchUser());
```


---

## login

Log in a user.

### Usage

```js
import { login } from '@shopgate/engage/user';

dispatch(login({login: 'user@email.com', password: 'password123'}, '/checkout', 'basic'));
```


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
