## App Info

The following example shows how to retrieve application information from storage:

```js
Promise<result> context.app.getInfo()
```

Example response:

```json
{
  "applicationId": "shop:10006",
  "deviceId": "r-671e5381-fc97-421c-9de0-99c9390c5bf9",
  "app": {
    "appVersion": "1.0.0",
    "codeBase": "2.0.0"
  }
}
```
