# Auth Step

Authentication is logging in or logging out a user from Shopgate CONNECT. Here are the required input/output objects for authentication:

| key | input/output | type | description |
|---|---|---|---|
| `userId`  | input (optional)  | string  | Specifies the user id provided by a login step before. When the value is empty, null, or undefined the previously logged in user is logged out. |
| `success`  | output  | boolean  | Indicates if login or logout is successful |

## Pipeline Example
The following example shows authentication for log in through a pipeline:

```json
...
{
  "type": "extension",
  "id": "shopgate/user",
  "path": "shopgate/user/login/loginToService.js",
  "input": [{"key": "strategy", "id": "1"}, {"key": "params", "id": "2"}],
  "output": [{"key": "userId", "id": "10", "optional": true}]
},
{
  "type": "auth",
  "input": [{"key": "userId", "id": "10", "optional": true}],
  "output": [{"key": "success", "id": "11"}]
}
...
```
