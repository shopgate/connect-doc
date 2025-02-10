---
stoplight-id: 6mzpovgmrhxx3
---

# Cart

## Cart Empty

These Portals are only available when the cart is empty. They wrap a graphical Element that renders on the Cart page.

| Name | Description | Props |
| - | - | - |
| `cart.empty.before` | Components are rendered **before** the Empty component of the cart. | none |
| `cart.empty` | Components **replace** the Empty component of the cart. | none |
| `cart.empty.after` | Components are rendered **after** the Empty component of the cart. | none |

## Cart Item List

These Portals are only available when the cart contains items.

| Name | Description | Props |
| - | - | - |
| `cart.item-list.before` | Components are rendered **before** the Cart Item List component. | none |
| `cart.item-list` | Components **replace** the Cart Item List component. | none |
| `cart.item-list.after` | Components are rendered **after** the Cart Item List component. | none |

## Cart Item

| Name | Description | Props |
| - | - | - |
| `cart.item.before` | Components are rendered **before** the Cart Item component. | `cartItem` -  The cart item data. |
| `cart.item` | Components **replace** the Cart Item component. | `cartItem` -  The cart item data. |
| `cart.item.after` | Components are rendered **after** the Cart Item component. | `cartItem` -  The cart item data. |

### Name

| Name | Description | Props |
| - | - | - |
| `cart.item.name.before` | Components are rendered **before** the cart item image. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.name` | Components **replace** the cart item name. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.name.after` | Components are rendered **after** the cart item name. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |

### Image

| Name | Description | Props |
| - | - | - |
| `cart.item.image.before` | Components are rendered **before** the cart item image. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.image` | Components **replace** the cart item image. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.image.after` | Components are rendered **after** the cart item image. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |

### Price

| Name | Description | Props |
| - | - | - |
| `cart.item.price.before` | Components are rendered **before** the cart item price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.price` | Components **replace** the cart item price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |
| `cart.item.price.after` | Components are rendered **after** the cart item price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (`product` or `coupon`) |

### Price Striked (only within products)

| Name | Description | Props |
| - | - | - |
| `cart.item.price-striked.before` | Components are rendered **before** the cart item strike price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `product` possible) |
| `cart.item.price-striked` | Components **replace** the cart item strike price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `product` possible) |
| `cart.item.price-striked.after` | Components are rendered **after** the cart item strike price. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `product` possible) |

### Coupon Code (only within coupons)

| Name | Description | Props |
| - | - | - |
| `cart.item.coupon-code.before` | Components are rendered **before** the code label within a cart item of type `coupon`. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `coupon` possible) |
| `cart.item.coupon-code` | Components  **replace** the code label within a cart item of type `coupon`. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `coupon` possible) |
| `cart.item.coupon-code.after` | Components are rendered **after** the code label within a cart item of type `coupon`. | `cartItemId` -  The ID of the current cart item.<br/>`type` - The type of the cart item (only `coupon` possible) |

## Coupon Input Field

| Name | Description | Props |
| - | - | - |
| `cart.coupon-field.before` | Components are rendered **before** the coupon input field. | none |
| `cart.coupon-field` | Components **replace** the coupon input field. | none |
| `cart.coupon-field.after` | Components are rendered **after** the coupon input field. | none |

## Payment Bar

These Portals are only available when the cart contains items and cart sums can be shown.

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.before` | Components are rendered **before** the PaymentBar component. | none |
| `cart.payment-bar` | Components **replace** the PaymentBar component. | none |
| `cart.payment-bar.after` | Components are rendered **after** the PaymentBar component. | none |

### Totals

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.before` | Components are rendered **before** the totals section of the Payment Bar. | none |
| `cart.payment-bar.totals` | Components **replace** the totals section of the Payment Bar. | none |
| `cart.payment-bar.totals.after` | Components are rendered **after** the totals section of the Payment Bar. | none |

#### Subtotal

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.sub-total.before` | Components are rendered **before** the subtotal row within the totals section. | none |
| `cart.payment-bar.totals.sub-total` | Components **replace** the subtotal row within the totals section. | none |
| `cart.payment-bar.totals.sub-total.after` | Components are rendered **after** the subtotal row within the totals section. | none |

#### Discounts

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.discounts.before` | Components are rendered **before** the discount row within the totals section. | none |
| `cart.payment-bar.totals.discounts` | Components **replace** the discount row within the totals section. | none |
| `cart.payment-bar.totals.discounts.after` | Components are rendered **after** the discount row within the totals section. | none |

#### Shipping

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.shipping.before` | Components are rendered **before** the shipping row within the totals section. | none |
| `cart.payment-bar.totals.shipping` | Components **replace** the shipping row within the totals section. | none |
| `cart.payment-bar.totals.shipping.after` | Components are rendered **after** the shipping row within the totals section. | none |

#### Tax

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.tax.before` | Components are rendered **before** the tax row within the totals section. | none |
| `cart.payment-bar.totals.tax` | Components **replace** the tax row within the totals section. | none |
| `cart.payment-bar.totals.tax.after` | Components are rendered **after** the tax row within the totals section. | none |

#### Grand Total

| Name | Description | Props |
| - | - | - |
| `cart.payment-bar.totals.grand-total.before` | Components are rendered **before** the grand total row within the totals section. | none |
| `cart.payment-bar.totals.grand-total` | Components **replace** the grand total row within the totals section. | none |
| `cart.payment-bar.totals.grand-total.after` | Components are rendered **after** the grand total row within the totals section. | none |

### Checkout Button

| Name | Description | Props |
| - | - | - |
| `cart.checkout-button.before` | Components are rendered **before** the CheckoutButton component. | `isActive` - Indicates if the checkout button is active. |
| `cart.checkout-button` | Components **replace** the CheckoutButton component. | `isActive` - Indicates if the checkout button is active. |
| `cart.checkout-button.after` | Components are rendered **after** the CheckoutButton component. | `isActive` - Indicates if the checkout button is active. |