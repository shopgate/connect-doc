# login

The `login` action uses the supplied developer account credentials (username and password) to authenticate against the Shopgate CONNECT platform. Both username and password can be specified as an option, but you are prompted for any missing information.

## Options

Name | Description
--- | ---
`--username` | The username of the developer account (usually an e-mail address)
`--password` | The password of the developer account

## Examples

```shell
sgconnect login
sgconnect login --username john.doe@example.com
sgconnect login --username jane.doe@example.com --password yawYuJaycMXnTYQLMUuaF4bU
```
