## Meta

The Meta object provides basic request information, such as the app id of the device where the request originated. The Meta object includes the following properties:

- **appId**: your application’s id
- **deviceId**: the current device id
- **userId**: the user’s id (if logged in, otherwise null)
- **headers**: HTTP request headers if pipeline request originated from browser; undefined if not from browser
- **cookies**: HTTP request cookies if pipeline request originated from browser; undefined if not from browser
