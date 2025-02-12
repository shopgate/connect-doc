---
stoplight-id: gsi5juh5uyhjd
---

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



## HTTP-Request Headers
```code
POST /shopgate/api.php HTTP/1.1
User-Agent: Shopgate
Host: yourshop.com
Accept: */*

X-Shopgate-Auth-User:  12345-1329146130
X-Shopgate-Auth-Token: b83e778fb008e0b006a4094787aba2d9543d6d25

Content-Length: 80
Content-Type: application/x-www-form-urlencoded
```

## Example implementation the authentication in PHP
```php
<?php
$customerNumber = "12345";
$apiKey         = "01677e4c0ae5468b9b8b823487f14524";
$timestamp      = time();

// Test if the X-headers were transmitted
if (empty($_SERVER['HTTP_X_SHOPGATE_AUTH_USER']) || empty($_SERVER['HTTP_X_SHOPGATE_AUTH_TOKEN'])) {
    throw new ShopgateLibraryException(
        ShopgateLibraryException::AUTHENTIFICATION_FAILED,
        'No authentication data present.'
    );
}

$name  = $_SERVER['HTTP_X_SHOPGATE_AUTH_USER'];
$token = $_SERVER['HTTP_X_SHOPGATE_AUTH_TOKEN'];

// Extract customer number and timestamp
$matches = array();
if (!preg_match('/(?<customer_number>[1-9][0-9]+)-(?<timestamp>[1-9][0-9]+)/', $name, $matches)) {
    throw new ShopgateLibraryException(
        ShopgateLibraryException::AUTHENTIFICATION_FAILED,
        'Cannot parse: '.$name.'.'
    );
}

$smaCustomerNumber = $matches["customer_number"];
$timestamp         = $matches["timestamp"];

// Test if the request is already older than 30 minutes
if ((time() - $timestamp) >= (30*60)) {
    throw new ShopgateLibraryException(
        ShopgateLibraryException::AUTHENTIFICATION_FAILED,
        'Request too old.'
    );
}

// "Rebuild" the authentication token
$generatedToken = sha1("SPA-{$smaCustomerNumber}-{$timestamp}-{$apiKey}");

// Test customer number and token
if (($smaCustomerNumber != $customerNumber) || ($token != $generatedToken)) {
    throw new ShopgateLibraryException(
        ShopgateLibraryException::AUTHENTIFICATION_FAILED,
        'Invalid authentication data.'
    );
}
?>
```