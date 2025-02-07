## Storage

Sometimes an extension or the step of an extension needs to store data or retrieve data from storage. Each storage type provides a simple key/value storage and a map storage. You can store any value (strings, numbers, arrays, objects) for a key. You can access complete maps or access items directly from map storage.

### callable as callback - or promise function
```javascript
void context.storage.<extension|device|user>.set(key, value, cb(err))
Promise context.storage.<extension|device|user>.set(key, value)
````

### set
```js
Promise context.storage.<extension|device|user>.set(key, value)
```

### get
```js
Promise<result> context.storage.<extension|device|user>.get(key)

```


### delete

```js
Promise context.storage.<extension|device|user>.del(key)
```

### set map
```js
Promise context.storage.<extension|device|user>.map.set(key, value)
```

### get map
```js
Promise<result> context.storage.<extension|device|user>.map.get(key)
```

### delete map
```js
Promise context.storage.<extension|device|user>.map.del(key)
```

### set item of map
```js
Promise context.storage.<extension|device|user>.map.setItem(mapId, indexId, value)
```

### get item of map
```js
Promise<result> context.storage.<extension|device|user>.map.getItem(mapId,
indexId)
```

### delete item of map
```js
Promise context.storage.<extension|device|user>.map.delItem(mapId,
indexId)
```

## Device Info
The following example shows how to retrieve device information from storage:

```js
Promise<result> context.device.getInfo()
```

Contains either “web” or “app” key.

Example response:

```json
{
  "clientType": "web/app",
  "deviceType": "phone/tablet",
  "screen": {
    "width": 768,
    "height": 1024,
    "scale": 1
  },
  "locale": "de",
  "preferredLanguages": [
    "de",
    "en"
  ],
  "app": {
    "model": "iPhone6,2",
    "os": {
      "platform": "ios",
      "ver": "8.1.3",
      "apiLevel": "8.1.3"
    },
    "carrier": "AT&T",
    "cameras": [{
      "light": true,
      "resolutionX": 1920,
      "resolutionY": 1080,
      "type": "front",
      "video": true
    }]
  },
  "web": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.155 Safari/537.36",
    "cookies": {
      "foo": "bar"
    }
  }
}
```

## App Info

The following example shows how to retrieve application information from storage:

```js
Promise<result> context.app.getInfo()
```

Example response:
```js
{
  "applicationId": "shop:10006",
  "deviceId": "r-671e5381-fc97-421c-9de0-99c9390c5bf9",
  "app": {
    "appVersion": "1.0.0",
    "codeBase": "2.0.0"
  }
}
```

### Meta
The Meta object provides basic request information, such as the app id of the device where the request originated. The Meta object includes the following properties:
- **appId**: your application’s id
- **deviceId**: the current device id
- **userId**: the user’s id (if logged in, otherwise null)
- **headers**: HTTP request headers if pipeline request originated from browser; undefined if not from browser
- **cookies**: HTTP request cookies if pipeline request originated from browser; undefined if not from browser
