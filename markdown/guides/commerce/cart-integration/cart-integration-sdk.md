# Cart Integration SDK

The Shopgate Cart Integration SDK is a compilation of classes to manage the communication between your shop system and Shopgate via the [Shopgate Plugin API](/guides/commerce/cart-integration/plugin-api) and the [Shopgate Merchant API](/guides/commerce/cart-integration/merchant-api). The SDK provides methods for processing incoming and outgoing requests, configuration options and for handling errors. The SDK also offers container classes, which allow easy storage of order data, among other things. Better like to start coding immediately? Have a look at the sample plugin code and get going! You're welcome to check back here anytime.

The most important functions are:
* Shopgate Plugin API, i.e. the communication interface for Shopgate
* implementation of the Shopgate Merchant API communication for your order management
* workflow mapping (data export, order import, etc.)
* an easy-to-use interface

## Download
* [Cart Integration SDK on Github](https://github.com/shopgate/cart-integration-sdk) 
* [Cart Integration SDK download](https://github.com/shopgate/cart-integration-sdk/releases/latest)
* [Example Plugin](/guides/commerce/cart-integration/example-plugin)

## Requirements
Following requirements must be met in order to use the Shopgate Cart Integration SDK:
- PHP version >= 5.2
- The PHP [max_execution_time](http://www.php.net/manual/en/info.configuration.php#ini.max-execution-time) setting must be at least 10 seconds (depending on the number of products).
- The PHP [memory_limit](http://www.php.net/manual/en/ini.core.php#ini.memory-limit) setting must be at least 20 MB (depending on the number of products).
- The CURL library for PHP must be installed in order to send requests to the Shopgate Merchant API.

## Layout for the Plugin
See chapter [Incoming Requests](/guides/commerce/cart-integration/sdk#incoming-requests) to learn how calls to the Shopgate Plugin API can be dispatched to your plugin. Your plugin class extends the ShopgatePlugin class of the SDK and must implement its abstract callback methods. Use the PHP constant `SHOPGATE_PLUGIN_VERSION` to store the current versions number of your plugin in the 2.x.x format. The first two numbers must be identical with the version number of the Shopgate Library you are using.

**Get the full [plugin example code](/guides/commerce/cart-integration/example-plugin) or have a look at the short example for a plugin class:**

## Example ShopgatePlugin Class
```php
 <?php
require_once(dirname(__FILE__).'/vendor/shopgate/cart-integration-sdk/shopgate.php'); // adjust this path to your environment
define('SHOPGATE_PLUGIN_VERSION', '2.9.0');

class ShopgatePluginMyShopSystem extends ShopgatePlugin {
    public function startup() {
        // ...
    }

    public function getCustomer($user, $pass) {
        // ...
    }

    public function registerCustomer($user, $pass, ShopgateCustomer $customer){
        // ...
    }

    public function addOrder(ShopgateOrder $order) {
        // ...
    }

    public function updateOrder(ShopgateOrder $order) {
        // ...
    }

    public function getOrders($customerToken, $customerLanguage, $limit = 10, $offset = 0, $orderDateFrom = '', $sortOrder = 'created_desc') {
        // ...
    }

    protected function createItems($limit = null, $offset = null, array $uids = array()) {
        // ...
    }

    protected function createReviews($limit = null, $offset = null, array $uids = array()) {
        // ...
    }
    
    protected function createCategories($limit = null, $offset = null, array $uids = array()) {
        // ...
    }

    public function cron($jobname, $params, &$message, &$errorcount) {
        // ...
    }

    public function checkCart(ShopgateCart $shopgateCart) {
        // ...
    }

    public function checkStock(ShopgateCart $shopgateCart) {
        // ...
    }

    public function getSettings() {
        // ...
    }

    public function syncFavouriteList($customerToken, $items) {
        // ...
    }
}
```


## Configuration
Using the components of the Shopgate Cart Integration SDK depends on configuration settings in many parts. The class ShopgateConfig is responsible for loading and saving these.
Advanced Implementation

To get all out of the new ShopgateConfig class you can extend it in order to add own validation rules, override the loading and saving procedures (e.g. to implement saving into a database instead of the file system) or define new default values.

A detailed description and examples can be found on the page [Cart Integration SDK: Configuration](/guides/commerce/cart-integration/sdk/configuration).
Quick Implementation

Create a file called myconfig.php inside the Shopgate Cart Integration SDK's config folder and define the $shopgate_config variable with your settings as shown below:

## Example myconfig.php
```php
TODO
```

## Incoming Requests
The starting point for requests of the Shopgate Plugin API depends on the shopping system. The starting point can be an independent script (e.g. api.php), a controller of the shop system, a hook point or something similar. Parameters are transmitted via POST. To receive GET parameters please contact out tech support.

> **⚠ Note:** Some requests, e.g. get_items, stop the execution of the script after the data file has been returned.

> **⚠ Note:** Outputting anything before or after the output of the Shopgate Cart Integration SDK can cause script errors or an invalid response to Shopgate.


## Outgoing Requests
In order to send a request, use the `ShopgateMerchantApi` object in your plugin class ($this->merchantApi) and run the required method. Parameters and response values can be found in the API documentation.
<br><br>API methods will throw a `ShopgateMerchantApiException` or `ShopgateLibraryException` in case of an error. Errors at critical points (e.g. during the checkout process or while editing an order) must not abort the script execution in any case. Errors of that kind only need to be logged.

*Sending requests to the Shopgate Merchant API when the status of an order changes.*

*Sending requests to the Shopgate Merchant API to fetch one order*

# Configuration

# Configuration

Since version 2.1.0 the Shopgate Library offers a revised version of the ShopgateConfig class with better support for expandability of modules. You can influence the configuration saving and loading behaviour as well as additional settings by deriving your own configuration class, for instance, in order to implement saving the configuration to a database.
Better like to start coding immediately? Simply download the [sample code](http://files.shopgate.com/wiki/example_shopgate_config.zip) and get going! You're welcome to check back here anytime.

## Attribute, Getter & Setter
Configuration settings are saved in class attributes. Access is performed via getter and setter methods.
The following conventions apply:

- Class attributes are protected. Do not use private!
- An attribute name consists of lowercase letters and underscores. Example: $enable_mobile_redirect
Names of the getter and setter methods for an attribute must be written in CamelCase. Example: `setEnableMobileRedirect($value)`, `getEnableMobileRedirect()`
- Attributes representing a configuration setting are initialized in the `startup()` method.

## Loading & Initializing
The following sequence is executed internally when the configuration is initialized:

1. Initialization of all attributes in the class ShopgateConfig.
2. The `startup()` method is called to initialize subclasses.
3. Loading of the passed array or the file `.../shopgate_library/config/myconfig.php`

If you want to implement your own method to load configuration values (e.g. `loadDatabase()`), you should call them in the `startup()` method. To keep the class from trying to initialize configuration from a file or through an array, return boolean true.
In order to load the configuration after the initialization, you can call the `loadArray()` or `loadFile()` methods at any time later. Their visibility is public.

## Saving
The configuration can be saved to a file with the `saveFile()` method. When doing that, keep in mind:

- Parameter 1 has to contain the list of fields to be saved. If no list is given, nothing will be saved.
- Parameter 2 contains the path to the file in which the configuration should be saved. If this parameter is null the class will try to use the `.../shopgate_library/config/myconfig.php` file to save the configuration..
- Parameter 3 indicates whether the saved data should (true) or should not (false) be validated.
- The method can throw a `ShopgateLibraryException` when saving or validation fails. You have to catch it.

You can implement your own method (e.g. `saveDatabase()`) if you do not want to save the configuration into a file. Your method should also throw a `ShopgateLibraryException` when errors occur during the saving process, so that they can be logged and displayed to the online shop user.

## Validating
For manual validation call the validate() method. You can use the $fieldList parameter with it. If the method does not return anything, the validation is successful. If the validation fails, it throws a `ShopgateLibraryException`.
Validation rules for the ShopgateConfig class configuration are contained in the `$coreValidations` attribute as regular expressions.

There are two ways to validate additional fields of your own configuration class:
1. Define your own regular expressions in the `$customValidations` attribute.
2. Implement the `validateCustom()` method.

Check the structure of the `$coreValidations` attribute to learn what the `$coreValidations` attribute has to look like. If regular expressions are insufficient for your purposes, you can define your own logic in `validateCustom()`. This method will be called automatically. Your return value must return a list of fields for which the validation failed or an empty array for a successful validation.
Both approaches can be combined.

## Examples
The following examples are divided by chapters, but always relate to the same sample class called *ShopgateConfigMyShoppingSystem*. You can download the complete [sample code](http://files.shopgate.com/wiki/example_shopgate_config.zip) here.

## Attribute, Getter & Setter
The sample class in the listing below creates additional configuration settings and introduces a database connection stored in the $db attribute. The connection will be used in the subsequent examples.

## Initializing
The `startup()` method in the following listing is an example to illustrate:

- Adding regular expressions for validation.
- Overwriting standard settings of the ShopgateConfig class.
- Initialization of the standard values for new settings.
- Loading the configuration through a custom method.
- Prevent further initialization of the ShopgateConfig class' default routines by returning true.

## Loading
The `loadDatabase()` method in the listing below is an example to illustrate:
- Initialization of the database connection (method initDatabase()).
- Loading the configuration from the database as a JSON string.
- Initialization with the values from the decoded JSON array.
- Appropriate error handling.

> **⚠ Attention:** The `ShopgateLibraryException` always needs to be caught in the front-end of the online shop when this method is called.

## Saving
The `saveDatabase()` method in the listing below is an example to illustrate:
- Validation of the configuration values to be saved.
- Initialization of the database connection (method initDatabase()).
- Conversion of the configuration into an array with toArray() and encoding it in JSON notation.
- Saving the created JSON string into the database.
- Appropriate error handling.

> **⚠ Attention:** The `ShopgateLibraryException` always needs to be caught in the front-end of the online shop when this method is called.

## Validating
Regular expressions contained in the `$customValidations` attribute will automatically be applied when the `validate()` method gets called. The following method can be used for validations that cannot be covered by regular expressions, or when you want to avoid using regular expressions.

The `validateCustom()` method in the following listing is an example to illustrate: 
- Going through the list of fields to be validated.
- A sample validation of the `$currency` and `$customer_group_id` settings.
- Returning names of the fields that failed validation or an empty array if validation was okay.

> **⚠ Attention:** This method is automatically called with the `validate()` method. There is no need to call it separately.

# Updating to a New Version

# Updating to a New Version

## Updating from 2.8.x to 2.9.x

1. **New method createReviews()**
The new method createReviews() representing the export of product reviews in the XML format needs to be implemented in your plugin.
2. **New export model Shopgate_Model_Review**
Use the new export model Shopgate_Model_Catalog_Review to export product reviews in the Shopgate XML format.

## Updating from 2.7.x to 2.8.x

1. **New method syncFavouriteList()**
The new method syncFavouriteList()representing the synchronization of a favourites list with Shopgate needs to be implemented in your plugin.
2. **New method getOrders()**
The new method getOrders() representing the export of orders to Shopgate needs to be implemented in your plugin.

## Updating from 2.6.x to 2.7.x

1. **ShopgateAuthentificationService replaced by two new classes**
This is most likely not relevant to you. Try a "ping" from admin.shopgate.com to your interface and try importing an order. If that still works, ignore this.

The class ShopgateAuthentificationService is now named ShopgateAuthenticationServiceShopgate.
The class ShopgateAuthenticationServiceOAuth was added for a state-of-the-art oAuth2 authentication process.

2. **ShopgateAuthentificationServiceInterface has been renamed**
The interface ShopgateAuthentificationServiceInterface has been renamed to ShopgateAuthenticationServiceInterface.

## Updating from 2.5.x to 2.6.x

1. **New method createCategories()**
The new method createCategories() representing XML export for categories needs to be implemented.
2. **New method createItems()**
The new method createItems() representing XML export for products needs to be implemented.

## Updating from 2.4.x to 2.5.x

1. **New method createMediaCsv()**
The new method createMediaCsv() representing the get_media_csv Method of the Shopgate Plugin API must be implemented.
2. **New method checkStock()()**
The new method checkStock() representing the check_stock Method of the Shopgate Plugin API must be implemented.

## Updating from 2.3.x to 2.4.x

1. **New method registerCustomer($user, $pass, ShopgateCustomer $customer)**
The new method registerCustomer($user, $pass, ShopgateCustomer $customer) representing the register_customer Method of the Shopgate Plugin API must be implemented.

## Updating from 2.2.x to 2.3.x

1. **New method getSettings()**
The new method getSettings() representing the get_settings action of the Shopgate Plugin API must be implemented.
2. **Changed default behaviour of ShopgateMerchantApi::addOrderDeliveryNote()**
The method's fifth parameter $sendCustomerMail now defaults to false! If you want an email to be sent to the customer by Shopgate this needs to be manually set to true now.

# Mobile Redirect

# Mobile Redirect

## Shopgate_Helper_Redirect_MobileRedirect
The Shopgate Library offers a class which already implements the [mobile redirect with the HTTP header](http://developer.shopgate.com/mobile_redirect#redirect-with-http-header) functionality in PHP.

> **⚠ Important:** There should not be any output before the header, or the redirect will fail.


## Redirecting Types
After setting the redirect target, you can call the appropriate method. For every redirecting type there is a method that instantly redirects the user if applicable (is using a smartphone, did not come back from the mobile website, ...) or builds the **Mobile Header** and SEO optimized 
**HTML tags** (see below).
- `buildScriptShop()`
<br>Redirecting to the Mobile Website homepage. If there is no mobile request, it returns the **Mobile Header**.
- `buildScriptItem($itemNumber)`
<br>Redirecting to a product on the Mobile Website by using the passed $itemNumber. If there is no mobile request, it returns the **Mobile Header**. The item number from the online shop is used as the parameter here.
- `buildScriptItemPublic($itemNumberPublic)`
<br>Redirecting to a product on the Mobile Website by using the passed $itemNumberPublic . If there is no mobile request, it returns the **Mobile Header**. The item number public from the online shop is used as the parameter here.
- `buildScriptCategory($categoryNumber)`
<br>Redirecting to a category on the Mobile Website. If there is no mobile request, it returns the **Mobile Header**. A category number from the online shop is used as the parameter here.
- `buildScriptBrand($brandName)`
<br>Redirecting to a brand on the Mobile Website. If there is no mobile request, it returns the **Mobile Header**. The name of the required brand is used as the parameter here.
- `buildScriptSearch($searchQuery)`
<br>Redirecting to a search for a product on the Mobile Website. If there is no mobile request, it returns the **Mobile Header**.The search term is used as the parameter here.
- `buildScriptCms($cmsPage)`
<br>Redirecting to a user-defined page on the Mobile Website. If there is no mobile request, it returns the **Mobile Header**. The internal name of the user-defined site is used as the parameter here.

## Mobile Header and Meta Tags
When a smartphone user returns to the desktop site, the Mobile Header must be displayed so the user can easily switch back to the mobile website.
Additionally a bunch of HTML meta tags must be displayed to hint search engine crawlers to the deeplinks on the mobile website and in the native apps, if available.

The JavaScript code and markup for this is returned by the buildScript*() methods explained above. It just needs to be inserted into an appropriate place in your template, view or layout.

## Open Graph Tags
On top of the Mobile Header and SEO meta tags Shopgate offers the integration of [Open Graph](http://ogp.me/) tags introduced by Facebook back in 2010. These are used to give social integrations more detailed information about a web site. If enabled, the tags are generated by the buildScript*() methods mentioned above along with the Mobile Header and meta tags.

Most of the Open Graph tags need parameters to be set or otherwise they won't be generated. To set a parameter, use the method `addSiteParameter($name, $value)`.

Valid values for $name can be found in the Shopgate_Helper_Redirect_TagsGeneratorInterface:: SITE_PARAMETER_* constants.
Please also see the [list of all currently supported parameters](/guides/commerce/cart-integration/sdk/open-graph-tags).

## Sample Application
The sample application of the class illustrates redirecting to the homepage and to the product and category levels. 

# Open Graph Tags

# Open Graph Tags

The class constants in the tables below refer to the constants in Shopgate_Helper_Redirect_TagsGeneratorInterface.

## General Site Parameters

Parameter Name|Class Constant|Description|Example
---|---|---|---
`sitename`|SITE_PARAMETER_SITENAME|The name of the desktop website.|My Awesome Shop
`desktop_url`|SITE_PARAMETER_DESKTOP_URL|The URL to the desktop site.|http://www.my-awesome-shop.com
`mobile_web_url`|SITE_PARAMETER_MOBILE_WEB_URL|The URL to the mobile website.|http://m.my-awesome-shop.com
`title`|SITE_PARAMETER_TITLE|The title of the currently viewed page.|My Awesome Shop - Genesis - Invisible Touch

## Product Detail Page Parameters

Parameter Name|Class Constant|Description|Example
---|---|---|---
`product_image`|SITE_PARAMETER_PRODUCT_IMAGE|The URL to a product image.|http://cdn.my-awesome-shop.com/images/products/CD-GENESIS-INV_TOUCH-1.png
`product_name`|SITE_PARAMETER_PRODUCT_NAME|The name of the product.|Genesis - Invisible Touch
`product_description_short`|SITE_PARAMETER_PRODUCT_DESCRIPTION_SHORT|A short (max. 140 characters) description of the product.|Invisible Touch is the thirteenth studio album from the English rock band Genesis.
`product_ean`|SITE_PARAMETER_PRODUCT_EAN|The European Article Number of the product.|0075678164125
`product_availability`|SITE_PARAMETER_PRODUCT_AVAILABILITY|One of "instock", "oos" or "pending" to indicate the availability of the product.|instock
`product_category`|SITE_PARAMETER_PRODUCT_CATEGORY|The name of the category this product is in.|80s rock / pop
`product_price`|SITE_PARAMETER_PRODUCT_PRICE|The (gross, if can be calculated) price of the product.|12.99
`product_currency`|SITE_PARAMETER_PRODUCT_CURRENCY|The currency the price is declared in.|$
`product_pretax_price`|SITE_PARAMETER_PRODUCT_PRETAX_PRICE|The net price of the product.|10.00
`product_pretax_currency`|SITE_PARAMETER_PRODUCT_PRETAX_CURRENCY|The currency the net price is declared in.|$


