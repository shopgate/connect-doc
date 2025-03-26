---
stoplight-id: 88tg249mmrjse
---

# Login
The Login page allows the user to either log in or to create a new account.

## How to customize
Main portals available on Login page are listed on [Login Page portals reference page](../portals/login-page.md).

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { LOGIN_PATH } from '@shopgate/engage/user';

const Component = () => (
    <Link href={LOGIN_PATH}>Open login page</Link>
);

export default Component;
```