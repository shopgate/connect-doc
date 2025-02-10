---
stoplight-id: l8d9no2n1ryl5
---

# Tracking Events and Data

This page lists all possible tracking events for which a tracking extension can register. Each event has a short description and an example of the data format required.  To learn more, refer to the Shopgate tutorial on [integrating a tracking provider](/tutorials/advanced/tracking-provider).

## Table of Contents

1. [General](#general)
2. [openDeepLink](#opendeeplink)
3. [openPushNotification](#opendeeplink)
4. [setCampaignWithUrl](#setcampaignwithurl)
5. [pageview](#pageview)
6. [viewContent](#viewcontent)
7. [search](#search)
8. [variantSelected](#variantselected)
9. [addToCart](#addtocart)
10. [loginSuccess](#loginsuccess)
11. [loginFailed](#loginfailed)
12. [initiatedCheckout](#initiatedcheckout)
13. [purchase](#purchase)

## General

Every event is called with four parameters (data, rawData, scope, state).

```javascript
this.register.eventName((data, rawData, scope, state) => {

});
```

| Parameter | Type | Description |
|-|-|-|
| `data` | *Object* | Preformatted event data.
| `rawData` | *Object* | The raw, not preformatted event data.
| `scope` | *Object* | Information about the event is supposed to be used by Shopgate internally only.
| `state` | *Object* | The complete redux state of the application at the time the event is triggered. Can be used to get additional data not included in data/rawData.

## openDeepLink

The `openDeepLink` event is triggered when the app opens from a deeplink.

| Key  | Description |
|-|-|
| `eventAction`  | URL of the deeplink. |
| `eventLabel`  | Indicates if the link comes from the spotlight search in iOS. |

### rawData

```json
  {
  eventAction: "testapp://category/123",
  eventLabel: "os_search"
}
```

### data

```json
{
  eventCategory: "",
  eventAction: "testapp://category/123",
  eventLabel: "os_search",
  eventValue: null,
  nonInteraction: false
}
```

## openPushNotification

The `openPushNotification` event is triggered when the app opens from a push notification.

| Key | Description  |
|-|-|
| `eventLabel` | The notification ID. |

### rawData

```json
{
  eventAction: "opened",
  eventLabel: "123"
}
```

### data

```json
{
  eventCategory: "",
  eventAction: "opened",
  eventLabel: "123",
  eventValue: null,
  nonInteraction: false
}
```

## setCampaignWithUrl

The `setCampaignWithUrl` event is triggered when the app opens from a deeplink or a push notification.

| Key | Description |
|-|-|
| `url` | URL of the deeplink or push notification. |
| `type` | "push_message" or "deeplink" |
| `[notificationId]`  | The push notification ID. Only set for push. |

### rawData & data

```json
{
  url: 'testapp://category/123',
  type: 'deeplink',
}
```

## pageview

The `pageview` event is triggered when any page is shown to the user.

### rawData

| Key | Description |
|-|-|
| `link` | The page URL. `https://rapid.shopgate.com/sg_app_resources/{shopNumber}/{name}/{params}` |
| `name` | Internal page name.  |

```json
{
  link: "https://rapid.shopgate.com/sg_app_resources/30694/item/123",
  name: "productDetails"
}
```

### data

| Key | Description |
|-|-|
| `merchantUrl` | Exact page identifier. |
| `shopgateUrl` | Identifier for Shopgate. |

```json
{
  merchantUrl: "item/123",
  shopgateUrl: "item"
}
```

### Pages Overview

| shopgateUrl | merchantUrl | name  | link |
|-|-|-|-|
| index | index | startpage | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/ |
| cart | cart | cart | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/cart |
| category | category/{categoryId} | productList | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/category/{categoryId} |
| item | item/{productId} | productDetails | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/item/{productId} |
| search | search?s={searchPhrase} | search | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/search?s={searchPhrase} |
| login | login | login | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/login |
| page | page/{pageId} | page | https://rapid.shopgate.com/sg_app_resources/{shopNumber}/page/{pageId} |

## viewContent

The `viewContent` event is triggered when a product page is shown.

### rawData

| Key | Description |
|-|-|
| `uid` | Product ID |
| `name` | Product name |
| `manufacturer` | Product manufacturer |
| `amount` | Object with price information |
| `amount.currency` | Currency code (ISO 4217)|
| `amount.gross` | Gross price|
| `amount.net` | Net price|
| `amount.striked` | Strike price|
| `tags` | Array with product tags |

```json
{
  amount: {
    currency: "EUR",
    gross: "140.00",
    net: "140.00",
    striked: "0.00"
  },
  manufacturer: "mcRonalds",
  name: "Product 4",
  tags: [],
  uid: "1003"
}
```

### data

| Key | Description |
|-|-|
| `id` | Product ID |
| `type` | Always "product"|
| `name` | Always "productDetails" |

```json
{
  id: "1003",
  type: "product",
  name: "productDetails"
}
```

## search

The `search` event is triggered when a search is performed.

### rawData

| Key | Description |
|-|-|
| `query` | The search query. |
| `resultCount` | Number of hits for the query. |

```json
{
  query: "test"
  resultCount: 160
}
```

### data

| Key | Description |
|-|-|
| `query` | Product ID |
| `hits` | Always "product"|
| `success` | Indicates if search results were found. |
| `type` | Always "product" |

```json
{
  hits: 160,
  query: "test",
  success: true,
  type: "product"
}
```

## variantSelected

The `variantSelected` event is triggered when a product variant gets selected. For example, "T-shirt size: L".

| Key | Description |
|-|-|
| `variant` | Object with information about the selected product variant.  |
| `baseProduct` |  Object with information about the base product. |

### rawData & data

```json
{
  baseProduct:{
    uid: "1013",
    name: "T-shirt",
    manufacturer: "",
    tags: [],
    amount:{
      net: "32.00",
      gross: "32.00",
      striked: "0.00",
      currency: "EUR"
    }
  },
  variant:{
    uid: "1013-1016",
    name: "T-shirt size L",
    manufacturer: "",
    tags: [],
    amount:{
      net: "32.00",
      gross: "32.00",
      striked: "0.00",
      currency: "EUR"
    }
  }
}
```

## addToCart

The `addToCart` event is triggered when a product is added to the cart.

### rawData

| Key | Description |
|-|-|
| `products` | Array with products added to the cart|
| `products[].uid` | Prduct ID|
| `products[].name` | Prduct name |
| `products[].manufacturer` | Product manufacturer |
| `products[].quantity` |  Quantity |
| `products[].amount` | Object with price information |
| `products[].amount.currency` | Currency code (ISO 4217)|
| `products[].amount.gross` | Gross price |
| `products[].amount.net` | Net price |
| `products[].amount.striked` | Striked price |

```json
{
  products:[{
    name: "T-shirt",
    manufacturer: "",
    tags: [],
    uid: "1013-1016",
    amount:{
      net: "32.00",
      gross: "32.00",
      striked: "0.00",
      currency: "EUR"
    },
    quantity: 1
  }]
}
```

### data

```json
{
  type:"product",
  items:[{
    id: "1013-1016",
    type: "product",
    name: "T-shirt",
    priceNet: 32,
    priceGross: 32,
    quantity: 1,
    currency: "EUR"
  }]
}
```

## loginSuccess

The `loginSuccess` event is triggered when a user has successfully logged in.

| Key | Description |
|-|-|
| `id` | User ID  |
| `mail` | User email address  |
| `firstName` | First name  |
| `lastName` | Last name  |
| `gender` | Gender (`male` or `female`)  |
| `birthday` | Date of birth  |
| `phone` | Phone number  |
| `customerGroups`  | Array with customer groups  |
| `addresses`  | Array with addresses of the user  |

### rawData & data

```json
{
  id: "87ddbbdb-5b09-4dc4-b1b0-214f4b0fdaa1",
  mail: "developer@shopgate.com",
  firstName: "John",
  lastName: "Doe",
  gender: "male",
  birthday: "2017-01-01",
  phone: "+1-800-490-2467",
  customerGroups: [{
    id: 3,
    name: "Retailer"
  }],
  addresses: [{
    id: 1,
    type: "invoice",
    firstName: "Jane",
    lastName: "Doe",
    company: "Shopgate Inc",
    street1: "804 Congress Ave.",
    street2: "string",
    city: "Austin",
    state: "TX",
    phone: "+1-800-490-2467",
    isDefault: true,
    alias: "Homeaddress",
    zipcode: "12345",
    country: "United States"
  }]
}
```

## loginFailed

The `loginFailed` event is triggered when the login of a user failed. **It does not receive any data.**

## initiatedCheckout

The `initiatedCheckout` event is triggered when the user enters the checkout.

### rawData

| Key | Description |
|-|-|
| `cart` | Object with information about the cart |
| `cart.amount` | Object with price information |
| `cart.amount.currency` | Currency code (ISO 4217)|
| `cart.amount.gross` | Gross price of the complete cart |
| `cart.productsCount` | Number of items in the cart |
| `cart.products[].uid` | Prduct ID |
| `cart.products[].name` | Product name |
| `cart.products[].quantity` | Quantity |
| `cart.products[].amount` | Object with price information |
| `cart.products[].amount.gross` | Gross price |

```json
{
  cart: {
  amount: {
    gross: "146.47",
    currency: "USD"
  },
  products: [{
    uid: "9209597131",
    name: "Seattle Mariners",
    amount: {
      gross: "34.99"
    },
    quantity: 2
  }],
  productsCount: 3
  }
}
```

### data

| Key | Description  |
|-|-|
| `currency` | Currency code (ISO 4217) |
| `valueGross` | Gross price of the complete cart |
| `valueNet` | Not available |
| `type` | Information about express checkout |
| `paymentInfoAvailable` | Indicates if the payment method is known. For example, PayPal Express. |

```json
{
  currency: "USD",
  numItems: 3,
  paymentInfoAvailable: false,
  type: "default",
  valueGross: 146.47,
  valueNet: undefined
}
```

## purchase

The purchase is triggered when an order was successfully placed and the user is redirected to the order confirmation page.

### rawData

| Key | Description |
|-|-|
| `number` | Unique order identifier |
| `currency` | Currency of the order |
| `totals` | Array of order totals |
| `totals[].type` | Total type (shipping, tax or grandTotal) |
| `totals[].amount` | Total amount with tax |
| `products` | Array of order items |
| `products[].id` | Product ID of the product or coupon code |
| `products[].name` | Product name |
| `products[].price.withTax` | Product gross price |
| `products[].price.net` | Item net price |
| `products[].quantity` | Item quantity |

```json
{
  order: {
    number: "1802332301",
    currency: "USD",
    totals [
      {
        type: "shipping",
        amount: 0
      },
      {
        type: "tax",
        amount: 12.44 // includes shipping tax, coupon tax and product tax
      },
      {
        type: "grandTotal",
        amount: 34.99
      }
    ],
    products: [
      {
        id: "9209597131",
        name: "Seattle Mariners",
        quantity: 1,
        price: {
          withTax: 34.99,
          net: 34.99
        }
      }
    ]
  }
}
```

### data

| Key | Description |
|-|-|
| `id` | Unique order identifier |
| `currency` | Currency of the order |
| `items` | Array of order items |
| `items[].type` | Item type. It can be `product` or `coupon`. |
| `items[].id` | Product ID of the product or coupon code |
| `items[].name` | Product name |
| `items[].priceGross` | Product gross price |
| `items[].priceNet` | Item net price |
| `items[].quantity` | Item quantity |
| `revenueGross` | Total gross revenue of the order |
| `revenueNet` | Total net revenue of the order |
| `shippingGross` | Gross amount of shipping |
| `shippingNet` | Net amount of shipping |
| `tax` | Amount of tax |

```json
{
  id: "1802332301",
  affiliation: "",
  currency : "USD",
  items: [{
    currency: "USD",
    id: "9209597131",
    name: "Seattle Mariners",
    priceGross: 34.99,
    priceNet: 34.99,
    quantity: 1,
    type: "product"
  }],
  revenueGross: 34.99,
  revenueNet: 34.99,
  shippingGross: 0,
  shippingNet: 0,
  tax: 0,
  type: "product"
}
```