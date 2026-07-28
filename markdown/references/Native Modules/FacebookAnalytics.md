---
stoplight-id: wzomtwpcdmlgz
---

# Facebook Analytics Module

The Facebook Analytics module records app events, purchases, push-notification opens, consent decisions, and user identity through the native Facebook SDK.

```jsx
import { FacebookAnalytics } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect } from 'react';
import { FacebookAnalytics } from '@shopgate/native-modules';

export function ProductViewTracker({ productId }) {
  useEffect(() => {
    const trackView = async () => {
      await FacebookAnalytics.logEvent({
        name: 'fb_mobile_content_view',
        eventParams: { fb_content_id: productId },
      });
    };
    trackView();
  }, [productId]);

  return null;
}
```

## analyticsSetConsent(params)

Enables or disables Facebook tracking according to the user's consent decision.

```jsx
function AcceptAnalyticsButton() {
  const accept = async () => FacebookAnalytics.analyticsSetConsent({ statistics: true, comfort: true });
  return <button type="button" onClick={accept}>Accept analytics</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `statistics` | `boolean` | yes | Whether statistics tracking is allowed. |
| `comfort` | `boolean` | no | Comfort consent value passed with the decision. |

## logEvent(params)

Logs a Facebook app event.

```jsx
function TrackEventButton() {
  const track = async () => FacebookAnalytics.logEvent({
    name: 'fb_mobile_content_view',
    valueToSum: 10,
    eventParams: { fb_content_id: 'product-1', fb_content_type: 'product' },
  });
  return <button type="button" onClick={track}>Track event</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `name` | `string` | yes | Facebook event name. |
| `valueToSum` | `number` | no | Numeric value associated with the event. |
| `eventParams` | `object` | no | Facebook event metadata with string or number values. |

## logPurchase(params)

Logs a purchase event.

```jsx
function TrackPurchaseButton() {
  const track = async () => FacebookAnalytics.logPurchase({
    purchaseAmount: 45,
    currencyCode: 'USD',
    eventParams: { fb_content_id: 'order-123' },
  });
  return <button type="button" onClick={track}>Track purchase</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `purchaseAmount` | `number` | yes | Purchase amount. |
| `currencyCode` | `string` | yes | ISO 4217 currency code. |
| `eventParams` | `object` | no | Additional purchase metadata. |

## logPushNotificationOpen(params)

Records that the app was opened from a Facebook push notification.

```jsx
function PushOpenButton({ payload }) {
  const track = async () => FacebookAnalytics.logPushNotificationOpen({ payload });
  return <button type="button" onClick={track}>Track push open</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `payload` | `object` | no | Push payload with string or number values. |

## setUserID(params)

Associates a custom user ID with Facebook events. Pass `null` to clear it.

```jsx
function SetFacebookUserButton() {
  const setUser = async () => FacebookAnalytics.setUserID({ userID: 'user-123' });
  return <button type="button" onClick={setUser}>Set Facebook user</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `userID` | `string \| null` | yes | User ID, or `null` to clear the current ID. |

All methods return `Promise<void>`.
