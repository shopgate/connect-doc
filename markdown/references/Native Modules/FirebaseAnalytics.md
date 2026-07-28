---
stoplight-id: uyo6o7vm0hetb
---

# Firebase Analytics Module

The Firebase Analytics module records standard ecommerce and engagement events and manages analytics consent, user IDs, and user properties through React Native Firebase Analytics.

```jsx
import { FirebaseAnalytics } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect } from 'react';
import { FirebaseAnalytics } from '@shopgate/native-modules';

export function ProductViewTracker({ productId }) {
  useEffect(() => {
    const trackView = async () => {
      await FirebaseAnalytics.logViewItem({
        item_id: productId,
        item_name: 'Example product',
        currency: 'USD',
        price: 12.5,
      });
    };
    trackView();
  }, [productId]);

  return null;
}
```

Event parameter objects accept custom keys with string, number, boolean, or item-array values. Standard Firebase Analytics keys include `item_id`, `item_name`, `item_category`, `currency`, `price`, `quantity`, `value`, `transaction_id`, and `search_term`.

## analyticsSetConsent(params)

Enables or disables analytics collection according to the user's consent decision.

```jsx
function AcceptAnalyticsButton() {
  const accept = async () => FirebaseAnalytics.analyticsSetConsent({ statistics: true });
  return <button type="button" onClick={accept}>Accept analytics</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `statistics` | `boolean` | yes | Whether analytics collection is allowed. |
| `comfort` | `boolean` | no | Comfort consent value passed with the decision. |

## Ecommerce events

The following methods accept an event-parameter object and return `Promise<void>`:

```jsx
function EcommerceButtons() {
  const addToCart = async () => FirebaseAnalytics.logAddToCart({
    item_id: 'ABC012345678',
    item_name: 'T-shirt',
    quantity: 3,
    price: 99.99,
    currency: 'USD',
  });

  const purchase = async () => FirebaseAnalytics.logEcommercePurchase({
    transaction_id: 'TR9876767ABC',
    value: 99.99,
    tax: 19,
    shipping: 15,
    currency: 'USD',
  });

  return (
    <>
      <button type="button" onClick={addToCart}>Add to cart</button>
      <button type="button" onClick={purchase}>Purchase</button>
    </>
  );
}
```

| Method | Typical parameters |
|--------|--------------------|
| `logAddPaymentInfo` | `currency`, `value`, `items`, `coupon` |
| `logAddToCart` | `item_id`, `item_name`, `quantity`, `price`, `currency` |
| `logAddToWishlist` | `item_id`, `item_name`, `price`, `currency` |
| `logBeginCheckout` | `transaction_id`, `value`, `currency`, `items` |
| `logEcommercePurchase` | `transaction_id`, `value`, `tax`, `shipping`, `currency`, `coupon` |
| `logViewItem` | `item_id`, `item_name`, `item_category`, `price`, `currency` |
| `logViewItemList` | `item_category`, `item_list_id`, `item_list_name`, `items` |

## Engagement events

```jsx
function EngagementButtons() {
  const logSearch = async () => FirebaseAnalytics.logSearch({ search_term: 'shirts' });
  const logLogin = async () => FirebaseAnalytics.logLogin({ method: 'email' });
  const logShare = async () => FirebaseAnalytics.logShare({ content_type: 'product', item_id: 'product-1', method: 'facebook' });

  return (
    <>
      <button type="button" onClick={logSearch}>Log search</button>
      <button type="button" onClick={logLogin}>Log login</button>
      <button type="button" onClick={logShare}>Log share</button>
    </>
  );
}
```

These methods accept event parameters and return `Promise<void>`: `logCampaignDetails`, `logLogin`, `logSearch`, `logSelectContent`, `logShare`, `logSignUp`, and `logViewSearchResults`.

## logEvent(name, params?)

Logs a custom Firebase event.

```jsx
function CustomEventButton() {
  const track = async () => FirebaseAnalytics.logEvent('my_own_event', {
    key1: 'string-example',
    key2: true,
    key3: 123,
  });
  return <button type="button" onClick={track}>Track custom event</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `name` | `string` | yes | Custom event name. |
| `params` | `object` | no | Event parameters. |

## User identity

```jsx
function UserAnalyticsButton() {
  const setUser = async () => {
    await FirebaseAnalytics.setUserId('user-123');
    await FirebaseAnalytics.setUserProperties({ account_type: 'premium' });
  };
  return <button type="button" onClick={setUser}>Set analytics user</button>;
}
```

### setUserId(id)

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `id` | `string \| null` | yes | User ID, or `null` to clear it. |

### setUserProperties(properties)

`properties` is an object whose values are `string` or `null`. Set a property to `null` to remove it.
