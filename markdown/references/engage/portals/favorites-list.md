---
stoplight-id: 3r9yx6vpcmcx5
---

# Favorites List

## Product Name

| Name | Description | Props |
| - | - | - |
| `favorites.product-name.before` | Components are rendered **before** the product name. | `product` - The product data |
| `favorites.product-name` | Components **replace** the product name. | `product` - The product data |
| `favorites.product-name.after` | Components are rendered **after** the product name. | `product` - The product data |

## Availability Text

| Name | Description | Props |
| - | - | - |
| `favorites.availability-text.before` | Components are rendered **before** the availability text. | `product` - The product data |
| `favorites.availability-text` | Components **replace** the availability text. | `product` - The product data |
| `favorites.availability-text.after` | Components are rendered **after** the availability text. | `product` - The product data |

## Product Price

| Name | Description | Props |
| - | - | - |
| `favorites.product-price.before` | Components are rendered **before** the product price. | `product` - The product data |
| `favorites.product-price` | Components **replace** the product price. | `product` - The product data |
| `favorites.product-price.after` | Components are rendered **after** the product price. | `product` - The product data |

## Add to Cart Button

| Name | Description | Props |
| - | - | - |
| `favorites.add-to-cart.before` | Components are rendered **before** the "Add to Cart Button" within a favorites list item. | none |
| `favorites.add-to-cart` | Components **replace** the "Add to Cart Button" within a favorites list item. | `handleAddToCart` - Adds the product to the cart.<br/>`productId` - The ID of the product.<br/>`isBaseProduct` - Indicates if the product is a "base product."<br/>`isDisabled` - Indicates if the button is supposed to be disabled. |
| `favorites.add-to-cart.after` | Components are rendered **after** the "Add to Cart Button" within a favorites list item. | none |