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

Header
```
POST /shopgate/api.php HTTP/1.1
User-Agent: Shopgate
Host: yourshop.com
Accept: */*

X-Shopgate-Auth-User:  12345-1329146130
X-Shopgate-Auth-Token: b83e778fb008e0b006a4094787aba2d9543d6d25

Content-Length: 80
Content-Type: application/x-www-form-urlencoded
```
Implementation
```php
$customerNumber = "12345";
$apiKey         = "01677e4c0ae5468b9b8b823487f14524";
$timestamp      = time();
 
// Test if the X-headers were transmitted
if (empty($_SERVER['HTTP_X_SHOPGATE_AUTH_USER']) || empty($_SERVER['HTTP_X_SHOPGATE_AUTH_TOKEN'])){
	throw new ShopgateLibraryException(
		ShopgateLibraryException::AUTHENTIFICATION_FAILED,
		'No authentication data present.'
	);
}
 
$name  = $_SERVER['HTTP_X_SHOPGATE_AUTH_USER'];
$token = $_SERVER['HTTP_X_SHOPGATE_AUTH_TOKEN'];
 
// Extract customer number and timestamp
$matches = array();
if (!preg_match('/(?<customer_number>[1-9][0-9]+)-(?<timestamp>[1-9][0-9]+)/', $name, $matches)){
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
```


# Stock Methods

## check_stock
Check current stock quantity of the product and returns available amount

### Specific Error Codes

| Code | Description | 
|---|---|
| 300 | product is not in stock | 
| 301 | product not found |  
| 302 | less stock available than requested |


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

# Export Methods
This four methods are probably the most important functions to implement in your shop system. These methods are used to setup a "copy" of your system in Shopgate. All data will be permanently updated within the Shopgate system by the import process.

## get_categories
This allows you to export item categories from your shop system to the Shopgate Categories XML Format.

### Plugin Example

```php
<?php
class MyPlugin extends ShopgatePlugin
    {
        ......
 
        protected function createCategories($limit = null, $offset = null, array $uids = array ())
        {
            /**
             * init category model
             */
            $categoryItem = new Shopgate_Model_Catalog_Category();
     
            $categoryItem->setUid(10);									        /** required */
            $categoryItem->setName('Example Category');						    /** required */
            $categoryItem->setParentUid(4);								        /** optional */
            $categoryItem->setIsActive(true);								    /** optional | default false */
            $categoryItem->setDeeplink('http://example-shop/category/id/10');   /** optional */
            $categoryItem->setIsAnchor(true);								    /** optional | default false */
            $categoryItem->setSortOrder(10);								    /** optional */
     
            /**
             * init image model
             */
            $imageItem = new Shopgate_Model_Media_Image();
     
            $imageItem->setUid(10);											        /** required */
            $imageItem->setSortOrder(10);									        /** optional */
            $imageItem->setAlt('Example Alt 1');								    /** optional */
            $imageItem->setUrl('http://example-shop/category/id/10/image/id/10');	/** optional */
            $imageItem->setTitle('Example Title 1');								/** required */
     
            /**
             * add to category model
             */
            $categoryItem->setImage($imageItem);
            $this->addCategoryModel($categoryItem);
        }
```

## get_items
This item allows you to export item information from your shop system to the Shopgate Items XML Format.
### Plugin Example
```php
<?
class MyPlugin extends ShopgatePlugin
{

    protected function createItems($limit = null, $offset = null, array $uids = array ())
    {

        /**
            * init product model
            */
        $productItem = new Shopgate_Model_Catalog_Product();
        
        $productItem->setUid(10);
        $productItem->setName('Example Product 1');
        $productItem->setTaxPercent(19);
        $productItem->setTaxClass('19% MwSt DE');
        $productItem->setCurrency('EUR');
        $productItem->setDescription('Example Description');
        $productItem->setDeeplink('http://example-shop/product/id/10/');
        $productItem->setPromotionSortOrder(10);
        $productItem->setInternalOrderInfo('Example Order Info');
        $productItem->setAgeRating(18);
        $productItem->setWeight(10);
        $productItem->setWeightUnit(Shopgate_Model_Catalog_Product::DEFAULT_WEIGHT_UNIT_GRAMM);
        
        ...........
        
        /**
            * add item 
            */
        $this->addItemModel($productItem);
```

#### Plugin Example Price
```php
<?
/**
    * init price model
    */
$priceItem = new Shopgate_Model_Catalog_Price();
$priceItem->setPrice(22.99);
$priceItem->setCost(12.99);
$priceItem->setMinimumOrderAmount(1);
$priceItem->setMsrp(18.99);
$priceItem->setSalePrice(21.99);

/**
    * init tier price (optional)
    */
$tierPriceItem = new Shopgate_Model_Catalog_TierPrice();
$tierPriceItem->setAggregateChildren(true);
$tierPriceItem->setCustomerGroupUid(1);
$tierPriceItem->setFromQuantity(10);
$tierPriceItem->setToQuantity(20);
$tierPriceItem->setReduction(5.99);
$tierPriceItem->setReductionType(Shopgate_Model_Catalog_TierPrice::DEFAULT_TIER_PRICE_TYPE_FIXED);

/**
    * add to price model
    */
$priceItem->addTierPriceGroup($tierPriceItem);

/**
    * init tier price (optional)
    */
$tierPriceItem = new Shopgate_Model_Catalog_TierPrice();
$tierPriceItem->setCustomerGroupUid(1);
$tierPriceItem->setFromQuantity(20);
$tierPriceItem->setToQuantity(30);
$tierPriceItem->setReduction(8.99);
$tierPriceItem->setReductionType(Shopgate_Model_Catalog_TierPrice::DEFAULT_TIER_PRICE_TYPE_FIXED);

/**
    * add to price model
    */
$priceItem->addTierPriceGroup($tierPriceItem);

/**
    * add to product model
    */
$productItem->setPrice($priceItem);
........
$this->addItemModel($productItem);
```

#### Plugin Example Images
```php
<?
/**
    * init image model
    */
$imageItem = new Shopgate_Model_Media_Image();
$imageItem->setUid(10);
$imageItem->setIsCover(true);
$imageItem->setSortOrder(10);
$imageItem->setAlt('Example Alt 1');
$imageItem->setTitle('Example Title 1');
$imageItem->setUrl('http://example-shop/product/id/10/image/id/10');

/**
    * add to product model
    */
$productItem->addImage($imageItem);

/**
    * init image model
    */
$imageItem = new Shopgate_Model_Media_Image();
$imageItem->setUid(20);
$imageItem->setIsCover(false);
$imageItem->setSortOrder(20);
$imageItem->setAlt('Example Alt 2');
$imageItem->setTitle('Example Title 1');
$imageItem->setUrl('http://example-shop/product/id/10/image/id/20');

/**
    * add to product model
    */
$productItem->addImage($imageItem);
```

#### Plugin Example Categories
```php
<?
/**
    * init category path model
    */
$categoryPathItem = new Shopgate_Model_Catalog_CategoryPath();
$categoryPathItem->setUid(10);
$categoryPathItem->setSortOrder(10);
$categoryPathItem->setDeeplink('http://example-shop/category/id/10');
$categoryPathItem->addItem(0, 'Home');
$categoryPathItem->addItem(1, 'Specials');

/**
    * add to product item
    */
$productItem->addCategoryPath($categoryPathItem);

/**
    * init category path model
    */
$categoryPathItem = new Shopgate_Model_Catalog_CategoryPath();
$categoryPathItem->setUid(20);
$categoryPathItem->setSortOrder(20);
$categoryPathItem->setDeeplink('http://example-shop/category/id/20');
$categoryPathItem->addItem(0, 'Home');
$categoryPathItem->addItem(1, 'Example 1');
$categoryPathItem->addItem(2, 'Example 2');

/**
    * add to product item
    */
$productItem->addCategoryPath($categoryPathItem);
```

#### Plugin Example Shipping
```php
<?
/**
    * init shipping model
    */
$shippingItem = new Shopgate_Model_Catalog_Shipping();
$shippingItem->setIsFree(false);
$shippingItem->setAdditionalCostsPerUnit(1.99);
$shippingItem->setCostsPerOrder(0.99);

/**
    * add to product model
    */
$productItem->setShipping($shippingItem);
```

#### Plugin Example Manufacturer
```php
<?
/**
    * init manufacturer model
    */
$manufacturerItem = new Shopgate_Model_Catalog_Manufacturer();
$manufacturerItem->setUid(10);
$manufacturerItem->setTitle('Shopgate');
$manufacturerItem->setItemNumber('sg');

/**
    * add to product
    */
$productItem->setManufacturer($manufacturerItem);
```

#### Plugin Example Visibility
```php
<?
/**
    * init visibility model
    */
$visibilityItem = new Shopgate_Model_Catalog_Visibility();
$visibilityItem->setLevel(Shopgate_Model_Catalog_Visibility::DEFAULT_VISIBILITY_CATALOG_AND_SEARCH);
$visibilityItem->setMarketplace(false);

/**
    * add to product model
    */
$productItem->setVisibility($visibilityItem);
```

#### Plugin Example Properties
```php
<?
/**
    * init property model
    */
$propertyItem = new Shopgate_Model_Catalog_Property();
$propertyItem->setUid(10);
$propertyItem->setLabel('Example Property 1');
$propertyItem->setValue('example value 1');

/**
    * add to product model
    */
$productItem->addProperty($propertyItem);

/**
    * init property model
    */
$propertyItem = new Shopgate_Model_Catalog_Property();
$propertyItem->setUid(20);
$propertyItem->setLabel('Example Property 2');
$propertyItem->setValue('example value 2');

/**
    * add to product model
    */
$productItem->addProperty($propertyItem);
```

#### Plugin Example Stock
```php
<?
/**
    * init stock model
    */
$stockItem = new Shopgate_Model_Catalog_Stock();
$stockItem->setStockQuantity(100);
$stockItem->setAvailabilityText('in stock');
$stockItem->setBackorders(true);
$stockItem->setIsSaleable(true);
$stockItem->setUseStock(true);
$stockItem->setMinimumOrderQuantity(1);
$stockItem->setMaximumOrderQuantity(10);

/**
    * add to product
    */
$productItem->setStock($stockItem);
```

#### Plugin Example Identifiers
```php
<?
/**
    * init identifier model
    */
$identifierItem = new Shopgate_Model_Catalog_Identifier();
$identifierItem->setUid(10);
$identifierItem->setType('EAN');
$identifierItem->setValue('00000001');

/**
    * add to product
    */
$productItem->addIdentifier($identifierItem);

/**
    * init identifier model
    */
$identifierItem = new Shopgate_Model_Catalog_Identifier();
$identifierItem->setUid(20);
$identifierItem->setType('EXAMPLE');
$identifierItem->setValue('e_2004_001');

/**
    * add to product
    */
$productItem->addIdentifier($identifierItem);
```

#### Plugin Example Tags
```php
<?
/**
    * init tag model
    */
$tagItem = new Shopgate_Model_Catalog_Tag();
$tagItem->setUid(10);
$tagItem->setValue('Example Tag 1');

/**
    * add to product model
    */
$productItem->addTag($tagItem);

/**
    * init tag model
    */
$tagItem = new Shopgate_Model_Catalog_Tag();
$tagItem->setUid(20);
$tagItem->setValue('Example Tag 2');

/**
    * add to product model
    */
$productItem->addTag($tagItem);
```

#### Plugin Example Relations
```php
<?
/**
    * init relation model
    */
$relationItem = new Shopgate_Model_Catalog_Relation();
$relationItem->setType(Shopgate_Model_Catalog_Relation::DEFAULT_RELATION_TYPE_CROSSSELL);
$relationItem->addValue(100);
$relationItem->addValue(102);

/**
    * add to product
    */
$productItem->addRelation($relationItem);

/**
    * init relation model
    */
$relationItem = new Shopgate_Model_Catalog_Relation();
$relationItem->setType(Shopgate_Model_Catalog_Relation::DEFAULT_RELATION_TYPE_CUSTOM);
$relationItem->setLabel('Custom Relation');
$relationItem->addValue(105);
$relationItem->addValue(109);

/**
    * add to product
    */
$productItem->addRelation($relationItem);
```

#### Plugin Example attributes Group
```php
<?
/**
    * init attribute group model
    */
$attributeGroupItem = new Shopgate_Model_Catalog_AttributeGroup();
$attributeGroupItem->setUid('10');
$attributeGroupItem->setLabel('Color');

/**
    * add to product model
    */
$productItem->addAttributeGroup($attributeGroupItem);

/**
    * init attribute group model
    */
$attributeGroupItem = new Shopgate_Model_Catalog_AttributeGroup();
$attributeGroupItem->setUid('20');
$attributeGroupItem->setLabel('Size');

/**
    * add to product model
    */
$productItem->addAttributeGroup($attributeGroupItem);
```

#### Plugin Example Inputs
```php
<?
/**
    * init inputs model
    */
$inputItem = new Shopgate_Model_Catalog_Input();
$inputItem->setUid(10);
$inputItem->setLabel('PDF upload');
$inputItem->setInfoText('Please select a pdf file');
$inputItem->setType(Shopgate_Model_Catalog_Input::DEFAULT_INPUT_TYPE_FILE);

/**
    * validation
    * init validation model
    */
$validationItem = new Shopgate_Model_Catalog_Validation();
$validationItem->setValidationType(Shopgate_Model_Catalog_Validation::DEFAULT_VALIDATION_FILE_PDF);

/**
    * add to input item
    */
$inputItem->setValidation($validationItem);

/**
    * add to product
    */
$productItem->addInput($inputItem);

/**
    * init inputs model
    */
$inputItem = new Shopgate_Model_Catalog_Input();
$inputItem->setUid(20);
$inputItem->setLabel('Select some Item');
$inputItem->setInfoText('Please select');
$inputItem->setType(Shopgate_Model_Catalog_Input::DEFAULT_INPUT_TYPE_SELECT);

/**
    * options
    *
    * init option model
    */
$optionModel = new Shopgate_Model_Catalog_Option();
$optionModel->setUid(10);
$optionModel->setLabel('Item 1');
$optionModel->setValue(1);
$optionModel->setAdditionalPrice(1.99);

/**
    * add to input model
    */
$inputItem->addOption($optionModel);

/**
    * init option model
    */
$optionModel = new Shopgate_Model_Catalog_Option();
$optionModel->setUid(20);
$optionModel->setLabel('Item 2');
$optionModel->setValue(2);
$optionModel->setAdditionalPrice(1.49);

/**
    * add to input model
    */
$inputItem->addOption($optionModel);

/**
    * validation
    * init validation model
    */
$validationItem = new Shopgate_Model_Catalog_Validation();
$validationItem->setValidationType(Shopgate_Model_Catalog_Validation::DEFAULT_VALIDATION_VARIABLE_INT);

/**
    * add to input item
    */
$inputItem->setValidation($validationItem);

/**
    * add to product
    */
$productItem->addInput($inputItem);

/**
    * init inputs model
    */
$inputItem = new Shopgate_Model_Catalog_Input();
$inputItem->setUid(20);
$inputItem->setLabel('Insert som text');
$inputItem->setInfoText('only numbers allowed');
$inputItem->setType(Shopgate_Model_Catalog_Input::DEFAULT_INPUT_TYPE_TEXT);

/**
    * init validation model
    */
$validationItem = new Shopgate_Model_Catalog_Validation();
$validationItem->setValidationType(Shopgate_Model_Catalog_Validation::DEFAULT_VALIDATION_TYPE_REGEX);
$validationItem->setValue('^[0-9]+$');

/**
    * add to input item
    */
$inputItem->setValidation($validationItem);

/**
    * add to product
    */
$productItem->addInput($inputItem);
```

#### Plugin Example Children
```php
<?
/**
    * init children model (product model)
    */
$childItem = new Shopgate_Model_Catalog_Product();
$childItem->setIsChild(true);

/**
    * attributes
    * init attribute model
    */
$attributeItem = new Shopgate_Model_Catalog_Attribute();
$attributeItem->setUid(10);
$attributeItem->setGroupUid(10);
$attributeItem->setLabel('red');

/**
    * add to child item
    */
$childItem->addAttribute($attributeItem);

/**
    * init attribute model
    */
$attributeItem = new Shopgate_Model_Catalog_Attribute(); 
$attributeItem->setUid(10);
$attributeItem->setGroupUid(20);
$attributeItem->setLabel('XXL');

/**
    * price
    * init price model
    */
$priceItem = new Shopgate_Model_Catalog_Price();

$priceItem->setPrice(18.88);

/**
    * add to child product
    */
$childItem->setPrice($priceItem);

/**
    * add to child item
    */
$childItem->addAttribute($attributeItem);

/**
    * you can extend / rewrite every property from the parent product
    * uid example
    */
$childItem->setUid('10_1');

/**
    * example name
    */
$childItem->setName('Example Product 1 (Child)');

/**
    * example identifier
    * init identifier model
    */
$identifierItem = new Shopgate_Model_Catalog_Identifier();

/**
    * uid from the parent identifier id
    */
$identifierItem->setUid(10);
$identifierItem->setValue('00000002');

/**
    * add to the child product
    */
$childItem->addIdentifier($identifierItem);
$productItem->addChild($childItem);
```

## get_reviews
This allows you to export reviews from your shop system to the Shopgate Categories XML Format.

### Plugin Example
```php
<?
class MyPlugin extends ShopgatePlugin
{
    ......

    protected function createReviews($limit = null, $offset = null, array $uids = array ())
    {
        /**
            * init review model
            */
        $reviewItem = new Shopgate_Model_Review();
    
        $reviewItem->setUid(10);									                        /** required */
        $reviewItem->setItemUid(312);	                            					    /** required */
        $reviewItem->setScore(6);								                            /** required */
        $reviewItem->setReviewerName('John Doe');								            /** required */
        $reviewItem->setDate('2007-08-25');                                                 /** optional */
        $reviewItem->setTitle('Great Product');								                /** optional */
        $reviewItem->setText('I would highly recommend to buy this product because...');    /** optional */

        $this->addReviewModel($reviewItem);
    }
```


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


# Cart Methods

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