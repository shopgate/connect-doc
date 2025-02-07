## Device Info

The following example shows how to retrieve device information from storage:

```js
Promise<result> context.device.getInfo()
```

Contains either “web” or “app” key.

Example response:

```json
{
  "clientType" : "web/app",
  "deviceType" : "phone/tablet",
  "screen" : {
    "width" : 768,
    "height" : 1024,
    "scale" : 1
  },
  "locale" : "de",
  "preferredLanguages" : [
    "de",
    "en"
  ],
  "app" : {
    "model": "iPhone6,2",
    "os" : {
      "platform": "ios",
      "ver": "8.1.3",
      "apiLevel": "8.1.3"
    },
    "carrier" : "AT&T",
    "cameras" : [
      {
        "light" : true,
        "resolutionX" : 1920,
        "resolutionY" : 1080,
        "type" : "front",
        "video" : true
      }
    ]
  },
  "web" : {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.155 Safari/537.36",
    "cookies" : {
      "foo" : "bar"
    }
  }
}
```
