---
stoplight-id: i9fyosn88rxn1
---

# Braze Module

The Braze module provides user identity, custom events, purchases, content cards, banners, push-permission requests, and user-attribute management through the native Braze SDK.

```jsx
import { Braze } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useState } from 'react';
import { Braze } from '@shopgate/native-modules';

export function BrazeControls() {
  const [banner, setBanner] = useState(null);

  const changeUser = async () => {
    await Braze.changeUser('user@example.com');
  };

  const loadBanner = async () => {
    await Braze.requestBannersRefresh(['dev-1']);
    setBanner(await Braze.getBannerIframe('dev-1'));
  };

  return (
    <div>
      <button type="button" onClick={changeUser}>Change user</button>
      <button type="button" onClick={loadBanner}>Fetch banner</button>
      {banner && <iframe title="Braze banner" srcDoc={banner.html} />}
    </div>
  );
}
```

## changeUser(userId, signature?)

Changes the active Braze user. The optional SDK signature is used when authenticated SDK access is enabled.

```jsx
function ChangeUserButton() {
  const changeUser = async () => Braze.changeUser('user-123', 'optional-sdk-signature');
  return <button type="button" onClick={changeUser}>Change user</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `userId` | `string` | yes | Braze user identifier. |
| `signature` | `string` | no | SDK authentication signature. |

## logCustomEvent(name, properties?)

```jsx
function CheckoutButton() {
  const trackCheckout = async () => Braze.logCustomEvent('completed_checkout', { orderId: '123' });
  return <button type="button" onClick={trackCheckout}>Track checkout</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `name` | `string` | yes | Custom event name. |
| `properties` | `object` | no | Event properties. |

`trackCustomEvent({ name, properties })` is also available when an object payload is preferred.

## logPurchase(productId, price, currencyCode, quantity?, purchaseProperties?)

```jsx
function PurchaseButton() {
  const trackPurchase = async () => Braze.logPurchase('sku-1', 12.5, 'USD', 1, { source: 'cart' });
  return <button type="button" onClick={trackPurchase}>Track purchase</button>;
}
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productId` | `string` | yes | Purchased product identifier. |
| `price` | `number` | yes | Unit price. |
| `currencyCode` | `string` | yes | ISO currency code. |
| `quantity` | `number` | no | Number of units. |
| `purchaseProperties` | `object` | no | Additional purchase properties. |

## Content cards

```jsx
import { useEffect, useState } from 'react';
import { Braze } from '@shopgate/native-modules';

export function ContentCardCount() {
  const [cards, setCards] = useState([]);

  useEffect(() => {
    const loadCards = async () => {
      await Braze.requestContentCardsRefresh();
      setCards(await Braze.getContentCards());
    };
    loadCards();
  }, []);

  return <p>Available cards: {cards.length}</p>;
}
```

`getContentCards()` returns current cards. `getCachedContentCards()` returns cached cards. Card interactions can be recorded with `logContentCardClicked`, `logContentCardImpression`, `logContentCardDismissed`, and `processContentCardClickAction`.

## Banners

```jsx
import { useRef } from 'react';
import { Braze } from '@shopgate/native-modules';

export function BannerContainer() {
  const containerRef = useRef(null);

  const fetchBanner = async () => {
    await Braze.requestBannersRefresh(['dev-1']);
    const banner = await Braze.getBannerIframe('dev-1');
    if (banner && containerRef.current) {
      containerRef.current.replaceChildren(banner.element);
    }
  };

  return (
    <div>
      <button type="button" onClick={fetchBanner}>Fetch banner</button>
      <div ref={containerRef} />
    </div>
  );
}
```

| Method | Parameters | Return value |
|--------|------------|--------------|
| `requestBannersRefresh` | `placementIds: string[]` | `Promise<void>` |
| `getBanner` | `placementId: string` | `Promise<BrazeBanner \| null>` |
| `getBannerIframe` | `placementId: string` | `Promise<BrazeBannerWithIframe \| null>` |
| `logBannerClick` | `banner`, optional `buttonId` | `Promise<void>` |

`getBannerIframe` returns `null` when no banner is available.

## User attributes and push permission

```jsx
function UpdateUserButton() {
  const updateUser = async () => {
    await Braze.setFirstName('Pascal');
    await Braze.setEmail('user@example.com');
    await Braze.setCustomUserAttribute({ key: 'tier', value: 'gold' });
    await Braze.addToSubscriptionGroup('newsletters');
    await Braze.requestPushPermission({ alert: true, badge: true, sound: true });
    await Braze.requestImmediateDataFlush();
  };
  return <button type="button" onClick={updateUser}>Update Braze user</button>;
}
```

`requestPushPermission` accepts optional `alert`, `badge`, `sound`, and `provisional` boolean options. Other user methods include aliases, date of birth, location, notification subscription types, custom arrays, and numeric custom-attribute increments.

## Events

### onBannerCardsUpdated

Fires when Braze finishes updating banner cards. The updated cards are available as `event.detail.banners`.

### onContentCardsUpdated

Fires when Braze finishes updating content cards. The updated cards are available as `event.detail.cards`.

```jsx
import { useEffect } from 'react';
import { Braze } from '@shopgate/native-modules';

export function BrazeUpdateListener() {
  useEffect(() => {
    const handleBanners = (event) => console.log('Banners updated', event.detail.banners);
    const handleCards = (event) => console.log('Cards updated', event.detail.cards);
    Braze.addEventListener('onBannerCardsUpdated', handleBanners);
    Braze.addEventListener('onContentCardsUpdated', handleCards);
    return () => {
      Braze.removeEventListener('onBannerCardsUpdated', handleBanners);
      Braze.removeEventListener('onContentCardsUpdated', handleCards);
    };
  }, []);
  return null;
}
```
