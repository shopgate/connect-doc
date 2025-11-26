---
stoplight-id: 125rcppe6rj6i
---

# User Selectors

* [getUserData](#getuserdata)
* [isUserLoggedIn](#isuserloggedin)
* [getUserDisplayName](#getuserdisplayname)
* [getUserFirstName](#getuserfirstname)
* [getUserEmail](#getuseremail)
* [isUserLoginDisabled](#isuserlogindisabled)
* [getRegisterUrl](#getregisterurl)

## getUserData

Retrieves the user data object from the store.

### Usage

```javascript
import { getUserData } from '@shopgate/engage/user';
```

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(Object|null)_: The user data. If no user data is found, it returns `null`.
> The user data will match the [getUser](../../../../static/pipelines/shopgate-user-pipelines.oas2.yml/paths/~1shopgate.user.getUser.v1/post) pipeline response.

---

## isUserLoggedIn

Retrieves whether the user is logged in from the user data in the store.

### Usage

```javascript
import { isUserLoggedIn } from '@shopgate/engage/user';
```



### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(boolean)_: Whether the user is logged in.

---

## getUserDisplayName

Retrieves the display name ({firstName} {lastName}) for a user from the user data in the store.

### Usage

```javascript
import { getUserDisplayName } from '@shopgate/engage/user';
```


### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The display name for a user. If no data is found, it returns `null`.

---

## getUserFirstName

Retrieves the first name for a user from the user data in the store.

### Usage

```javascript
import { getUserFirstName } from '@shopgate/engage/user';
```


### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The first name for a user. If no data is found, it returns `null`.

---

## getUserEmail

Retrieves the email for the currently logged in user.

### Usage

```javascript
import { getUserEmail } from '@shopgate/engage/user';
```


### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The email for the user. If no data is found, it returns `null`.

---

## isUserLoginDisabled

Retrieves whether the user login is disabled from the user data in the store.

### Usage

```javascript
import { isUserLoginDisabled } from '@shopgate/engage/user';
```


### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(boolean)_: Whether the user login is disabled.

---

## getRegisterUrl

Retrieves the registration URL from the data in the store.

### Usage

```javascript
import { getRegisterUrl } from '@shopgate/engage/user';
```


### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The registration URL. If no URL is found, it returns `null`.