# Plugin API

The Shopgate Plugin API is an interface that your shop system can provide for Shopgate. E.g. you can automatize the export of items or the import of Shopgate orders in your shop system. You also need the interface to register your shop's customers via "Shopgate Connect".

The Shopgate Plugin API is implemented by your shop system to enable Shopgate to communicate with it . It offers the following functions:
* XML data files retrieval
* new order notifications
* order change notifications
* status information transmission
* customer data transmission, especially via single sign-on

## Using the API

As a basic principle, the Shopgate plugin API is only executed by Shopgate. Parameters are transmitted via POST. If there are any problems with your shop system or the server when transmitting POST, please contact our support team.

The API always returns an array in JSON (possibly interlaced). The "error" field is of particular importance as it indicates whether the request was successful. If the API request was successful, the response field takes the value of 0. In case the request was not successful, an "error_text" containing a description of the error code is returned as well. A complete error list can be found under individual Methods.

## Testing

To test the Shopgate Plugin API, request a demo at Shopgate or use a POST client like [Postman](https://www.getpostman.com/) with example requests provided.

# Authentication

In order to prevent incoming requests of unauthorized third parties, Shopgate needs to be authenticated by the Shopgate plugin API in every request.

Two "X headers" containing a user name and auth token are sent along with every request.

- **X-Shopgate-Auth-User**
- **X-Shopgate-Auth-Token**

## User Name Generation
The user name is a combination of the following values:

1. Customer number
2. Unix timestamp

Both values are separated by a hyphen (-):

**Auth User**: `<Customer number>-<Unix timestamp>`
<br>**Example:** <span style="color:red">12345</span>-<span style="color:blue">1329146130</span>

## Auth Token Generation

The Auth Token is composed of the following parameters:

1. "SPA" string
2. Customer number
3. Current Unix timestamp
4. API key

is performed in the following way:
1. Separate the string with hyphens, e.g. `SPA-12345-1329146130-01677e4c0ae5468b9b8b823487f14524`
2. Use it as base for generating the SHA1 hash: `sha1(SPA-12345-1329146130-01677e4c0ae5468b9b8b823487f14524)`
3. The result is the Auth token (as SHA1 hash): `b83e778fb008e0b006a4094787aba2d9543d6d25`

# Stock

# Stock Method

## check_stock
Check current stock quantity of the product and returns available amount

### Specific Error Codes

| Code | Description | 
|---|---|
| 300 | product is not in stock | 
| 301 | product not found |  
| 302 | less stock available than requested |

# Order

# Order Methods
These methods are uses to update the payment and shipping statuses of orders and add orders to your shop system.

## add_order
With this action you can add a new Shopgate order to your shop system. If there already is an order with the same number, the action must cancel and the error must be reported.

### Specific Error Codes
| Code | Description | 
|---|---|
| 30 | parameter "order_number" missing | 
| 60 | duplicate order |  
| 62 | no customer group found for customer |
| 64 | order status is sent |
| 84 | unknown country code |
| 85 | unknown state code |

> **⚠ Attention:** If you DON'T use the Shopgate Library you also have to call our Shopgate Merchant API method `get_orders` to get the order data.

## get_orders
This action implements retrieval of order data from your shop. If a customer already has an account in your online shop, you can allow them to see the current status of their orders on the mobile website or in the mobile apps.

## update_order
With this action you can update an already existing Shopgate order in your shop system. In case that the order number is unknown, the action must be cancelled and the error reported.

### Specific Error Codes

| Code | Description | 
|---|---|
| 30 | parameter "order_number" missing | 
| 61 | order not found |  
| 64 | order status is sent |
| 65 | order is already up to date |

# Export

# Export Methods
This four methods are probably the most important functions to implement in your shop system. These methods are used to setup a "copy" of your system in Shopgate. All data will be permanently updated within the Shopgate system by the import process.

## get_categories
This allows you to export item categories from your shop system to the Shopgate Categories XML Format.

### Plugin Example

## get_items
This item allows you to export item information from your shop system to the Shopgate Items XML Format.
### Plugin Example

#### Plugin Example Price

#### Plugin Example Images

#### Plugin Example Categories

#### Plugin Example Shipping

#### Plugin Example Manufacturer

#### Plugin Example Visibility

#### Plugin Example Properties

#### Plugin Example Stock

#### Plugin Example Identifiers

#### Plugin Example Tags

#### Plugin Example Relations

#### Plugin Example attributes Group

#### Plugin Example Inputs

#### Plugin Example Children

## get_reviews
This allows you to export reviews from your shop system to the Shopgate Categories XML Format.

### Plugin Example

# Customer

# Customer Methods
These methods are responsible for transmitting customer data and registering new customers. They are also used to update shipping or billing address, setting additional data like birthday, phone or mobile number as well as email address.

## get_customer
This action implements retrieval of user data from your shop, e.g. for the "Shopgate Connect" procedure. If a customer already has an account in your online shop, you can allow them to use their credentials to log in, register and place orders on the mobile website.

### Specific Error Codes

| Code | Description | 
|---|---|
| 35 |  parameter "user" missing | 
| 36 | parameter "pass" missing |  
| 37 | parameter "user_data" missing |
| 70 |  no addresses found for customer | 
| 71 | wrong username or password |  
| 72 | customer account not confirmed |
| 73 | unknown error while customer login | 

## register_customer
This method allows a customer to be registered in your shop system.

### Specific Error Codes

| Code | Description |   
|---|---|
| 35 | parameter "user" missing | 
| 36 | parameter "pass" missing |  
| 37 | parameter "user_data" missing |
| 70 | no addresses found for customer | 
| 71 | wrong username or password |  
| 220 | failed to create user |
| 221 | user already exists |
| 222 | data fields are missing |

# Cart

# Cart Method

## check_cart
Every time a customer changes the contents of the cart in the Mobile Website or apps this action will be requested to validate the contents.
This is currently used to validate **coupons**, check the **stock** of the items and return **shipping service providers** of the shopping cart system. Future applications include a change of products for the cart contents.

### Coupon Error Codes

| Code | Description | 
|---|---|
| 200 | the coupon is not valid| 
| 201 | the coupon code is not valid |  
| 202 | products for coupon are not valid |
| 203 | delivery address for coupon is not valid | 
| 204 | user is not valid for coupon |  
| 205 | too many coupons in cart |

### Item Error Codes

| Code  | Description |
|---|---|
| 300 | product is not in stock |
| 301 | product not found |
| 302 | less stock available than requested |
| 303 | product input validation failed: text too long |
| 304 | requested quantity is lower than required minimum quantity |
| 305 | requested quantity is higher than allowed maximum quantity |
| 206 | products can not be ordered together |
| 207 | product not allowed in cart constellation |

# System Info

# System Info Methods
The following features allow simple custodial tasks to be completed through the Shopgate plugin.

## ping
Returns information about the framework and server used.

## get_settings
This action returns settings of an online store, e.g. the tax settings.

## set_settings
Used to make changes to settings, e.g. in the Shopgate configuration

### Specific Error Codes

| Code | Description | 
|---|---|
| 50 | parameter "shopgate_settings" missing | 

## get_log_file
This action allows access to the log files.

### Specific Error Codes

| Code | Description | 
|---|---|
| 38 | unknown log type | 

## clear_cache
This action allows the clearing of the cache folder.

### Specific Error Codes

| Code | Description | 
|---|---|
| 79 | cannot delete file(s) | 

## clear_log_file
This action allows clearing existing cache files.

### Specific Error Codes

| Code | Description | 
|---|---|
| 38 | unknown log type |

# General Error Codes

# General Error Codes

| Code  | Description | 
|---|---|
| 2 |  cannot open/create logfile(s) | 
| 10 | invalid value in configuration |  
| 11 | error reading or writing configuration |
| 20 | no action specified | 
| 21 | unknown action requested |  
| 22 | disabled action requested |
| 23 | wrong response format |
| 83 | database error |
| 100 | no connection to server | 
| 101 | Unknown action |  
| 102 | error code received from merchant API |
| 120 | authentication failed | 
| 999 | Unknown error | 