# Quick Start


 ## Example Plugin 

 You want to start developing with the Shopgate
 Cart Integration SDK here and now? You have come
 to the right place. Download the Shopgate Cart
 Integration SDK code from
 [here](https://github.com/shopgate/cart-integration-sdk/releases/latest).
 Extract the contents to the destination directory
 and create a `plugin.php` file in it. The file
 should contain the following code:


 ```php
<?php
require_once(dirname(__FILE__).'/vendor/shopgate/cart-integration-sdk/shopgate.php');
define('SHOPGATE_PLUGIN_VERSION', '2.9.0');
 
/**
 * Connection to Shopgate
 */
class ShopgatePluginMyShoppingSystem extends ShopgatePlugin {
	/**
	 * Callback function for initialization by plugin implementations.
	 *
	 * This method gets called on instantiation of a ShopgatePlugin child class and serves as __construct()
	 * replacement.
	 *
	 * Important: Initialize $this->config here if you have your own config class.
	 *
	 * @see http://developer.shopgate.com/library
	 */
	public function startup() {
		// Prepare and set up your stuff here. This function is always called before any other.
 
		// If you use Shopgate Library above 2.1 and a extended ShopgateConfig class, you need to set it here
		$this->config = new ShopgateConfigMyShoppingSystem();
	}
 
	/**
	 * This performs the necessary queries to build a ShopgateCustomer object for the given log in credentials.
	 *
	 * The method should not abort on soft errors like when the street or phone number of a customer can't be
	 * found.
	 *
	 * @see http://developer.shopgate.com/plugin_api/customers/get_customer
	 *
	 * @param string $user The user name the customer entered at Shopgate Connect.
	 * @param string $pass The password the customer entered at Shopgate Connect.
	 * @return ShopgateCustomer A ShopgateCustomer object.
	 * @throws ShopgateLibraryException on invalid log in data or hard errors like database failure.
	 */
	public function getCustomer($user, $pass) {
		// Database connection can be established here.
		// Check if the user's e-mail address ($user) and password ($pass) exist in the shop.
		// If user data is available, save them in, for instance, the $dbCustomerData array.
 
		// If there is no user or the password is wrong:
		if ($userNotFoundOrPasswordIsWrong) {
			throw new ShopgateLibraryException(
				ShopgateLibraryException::PLUGIN_WRONG_USERNAME_OR_PASSWORD,
				'User: '.$user
			);
		}
 
		// Additionally, retrieve user addresses and save them in, for instance, the $dbCustomerAddresses array:
		foreach ($dbCustomerAddresses as $dbCustomerAddress) {
			$address = new ShopgateAddress();
			$address->setId($dbCustomerAddress['address_id']);
			$address->setAddressType(($dbCustomerAddress['type'] == 'delivery_address'
				? ShopgateAddress::DELIVERY
				: ShopgateAddress::INVOICE
			));
			// Alternatively, if the invoice and shipping address is the same:
			// ShopgateAddress::BOTH
			$address->setGender($dbCustomerAddress['gender']);
			$address->setFirstName($dbCustomerAddress['firstname']);
			// ...
 
			$addresses[] = $address;
		}
 
		// If the user exists:
		$customer = new ShopgateCustomer();
		$customer->setCustomerId($dbCustomerData['customers_id']);
		$customer->setCustomerNumber($dbCustomerData['customers_cid']);
		// ...
 
		// An alternative if you don't want to publish the database ID of a customer
		// AND MANDATORY for the sync_favourite_list and get_orders actions:
		// Use a "customer token" to identify the user, this may be a hash of customer number,
		// name and time or whatever suits your needs best.
		$customer->setCustomerToken($dbCustomerData['customers_random_token']);
 
		// Important! Addresses need to be assigned to the customer here
		$customer->setAddresses($customerAddresses);
 
		return $customer;
	}
 
	/**
	 * Checks the content of a cart to be valid and returns necessary changes if applicable.
	 *
	 * This currently only supports the validation of coupons.
	 *
	 * @see http://developer.shopgate.com/plugin_api/cart
	 *
	 * @param ShopgateCart $cart The ShopgateCart object to be checked and validated.
	 * @return array(
	 *		'external_coupons' => ShopgateExternalCoupon[], # list of all coupons
	 *		'items' => array(...), # list of item changes (not supported yet)
	 *		'shippings' => array(...), # list of available shipping services for this cart (not supported yet)
	 * )
	 * @throws ShopgateLibraryException if an error occurs.
	 */
	public function checkCart(ShopgateCart $shopgateCart) {
		// Database connection can be established here
 
		// Create a cart in your shopping system solution and add all items and coupons
		$shopCart = new ShopCart();
 
		foreach ($shopgateCart->getItems() as $item) {
			$shopCart->addItem(array(
					'article_number' => $item->getItemNumber(),
					'article_name' => $item->getName(),
					// ...
			));
		}
 
		$validatedCoupons = array();
		foreach ($shopgateCart->getExternalCoupons() as $coupon) {
			try {
				$shopCart->addCoupon($coupon->getCode());
				$coupon->setIsValid(true);
			} catch (Exception $e) {
				$coupon->setIsValid(false);
				$coupon->setNotValidMessage($e->getMessage());
			}
 
			$validatedCoupons[] = $coupon;
		}
 
		return array(
			'external_coupons' => $validatedCoupons,
			'currency' => $shopgateCart->getCurrency(),
		);
		
	}
 
	/**
	 * Performs the necessary queries to add an order to the shop system's database.
	 *
	 * @see http://developer.shopgate.com/merchant_api/orders/get_orders
	 * @see http://developer.shopgate.com/plugin_api/orders/add_order
	 *
	 * @param ShopgateOrder $order The ShopgateOrder object to be added to the shop system's database.
	 *
	 * @return array(
	 *		'external_order_id' => string, # the ID of the order in your shop system's database
	 *		'external_order_number' => string, # the number of the order in your shop system
	 * )
	 * @throws ShopgateLibraryException if an error occurs.
	 */
	public function addOrder(ShopgateOrder $order) {
		// The database connection can be established here
 
		// Check if an order with the number ($order->getOrderNumber()) has already been imported from Shopgate
 
		// If an order is found with the order number ($order->getOrderNumber()) abort:
		if (!empty($dbOrder)) {
			throw new ShopgateLibraryException(ShopgateLibraryException::PLUGIN_DUPLICATE_ORDER);
		}
 
		// Has the order been placed by an existing customer?
		// Check if a user with the $customerId already exists and save the order together with the user
		$customerId = $order->getExternalCustomerId();
 
		// If a user does not exist: create a guest account in the shop system
		// ...
 
		// A simplified example of saving an order
		$shopOrder = new ShopOrder();
		$shopOrder->setCompleteAmountWithTax($order->getAmountComplete());
		$shopOrder->onHold($order->getIsShippingBlocked()); // set the order on hold if shipping is blocked
		$shopOrder->isPaid($order->getIsPaid());
		$shopOrder->setShopgateOrderNumber($order->getOrderNumber());
		// ...
 
		$orderId = $shopOrder->save();
		$orderNumber = $shopOrder->getOrderNumber();
 
		// Save the ordered items to the order
		$orderItems = $order->getItems();
		foreach ($orderItems as $orderItem) {
 
			$shopOrderItem = new ShopOrderItem();
			$shopOrderItem->setOrderId($orderId);
			$shopOrderItem->setArticleNumber($orderItem->getItemNumber());
			$shopOrderItem->setProductsPrice($orderItem->getUnitAmountWithTax());
			$shopOrderItem->setQuantity($orderItem->getQuantity());
			$shopOrderItem->setTax($orderItem->getTaxPercent());
			// ...
 
			$shopOrderItem->save();
 
		}
 
		// Retrieve addresses
		$delivery = $order->getDeliveryAddress();
		$invoice = $order->getInvoiceAddress();
 
		// Save addresses to the order
		// ...
 
		// Save payment specific data
		// http://wiki.shopgate.com/Merchant_API_payment_infos/de#SHOPGATE_2
		$paymentInfos = $order->getPaymentInfos();
		switch ($order->getPaymentMethod()) {
			case ShopgateOrder::SHOPGATE:
				// Payment Method: Shopgate
				// This covers all the payment methods settled via Shopgate
 
				break;
			case ShopgateOrder::PREPAY:
				// Payment Method: Prepayment
 
				// Reference number:
				$paymentInfos['purpose'];
 
				break;
			case ShopgateOrder::INVOICE:
				// Payment Method: Invoice
 
				break;
			case ShopgateOrder::DEBIT:
				// Payment Method: Direct Debit
 
				$paymentInfos["bank_account_holder"];
				$paymentInfos["bank_account_number"];
				$paymentInfos["bank_name"];
				$paymentInfos["bank_code"];
 
				break;
			case ShopgateOrder::COD:
				// Payment Method: Cash on Delivery
 
				break;
			case ShopgateOrder::DT_CC:
				// Payment Method: DataTrans Credit Card
 
				$paymentInfos["upp_transaction_id"];
				$paymentInfos["authorization"];
				$paymentInfos["settlement"];
				break;
			case ShopgateOrder::BILLSAFE:
				// Payment Method: Billsafe
 
				$paymentInfos["billsafe_transaction_id"];
				break;
			case ShopgateOrder::KLARNA_INV:
				// Payment Method: Klarna
 
				$paymentInfos["reservation_number"];
 
				break;
			default:
 
				// When no concrete payment method processing is possible/successful,
				// register the payment as mobile_payment and enter PaymentInfos
				// as a comment. PaymentInfos always contains the
				// name of the payment type as (shopgate_payment_name) field
 
				$paymentType = 'mobile_payment';
 
				$comment = '';
				foreach ($paymentInfos as $key => $value) {
					$comment .= $key.': '.$value."\n";
				}
 
				// save comments to the order
 
				break;
		}
 
		// Return the order ID and number of the order saved to the database
		return array(
			'external_order_id' => $orderId,	// used to inform a developer in case there was a problem
			'external_order_number' => $orderNumber // used to inform a merchant in case there was a problem
		);
	}
 
	/**
	 * Performs the necessary queries to update an order in the shop system's database.
	 *
	 * @see http://developer.shopgate.com/merchant_api/orders/get_orders
	 * @see http://developer.shopgate.com/plugin_api/orders/update_order
	 *
	 * @param ShopgateOrder $order The ShopgateOrder object to be updated in the shop system's database.
	 * @return array(
	 *		'external_order_id' => <i>string</i>, # the ID of the order in your shop system's database
	 *		'external_order_number' => <i>string</i> # the number of the order in your shop system
	 *	)
	 * @throws ShopgateLibraryException if an error occurs.
	 */
	public function updateOrder(ShopgateOrder $order) {
		// The database connection can be established here
 
		// Check if the order in question has already been imported into the system
		// with the Shopgate order number ($order->getOrderNumber()).
 
		// the order cannot be found in the system:
		if ($dbOrder == false) {
			throw new ShopgateLibraryException(
				ShopgateLibraryException::PLUGIN_ORDER_NOT_FOUND,
				"Shopgate order number: '{$order->getOrderNumber()}'."
			);
		}
 
		if ($order->getUpdatePayment() == 1) {
			// Payment status or PaymentInfos has changed
 
			$order->getIsPaid();
			$order->getPaymentInfos();
 
		}
 
		if ($order->getUpdateShipping() == 1) {
			// Released or blocked for shipping
 
			$order->getIsShippingBlocked();
		}
 
		// Return the order ID and number of the order saved to the database
		return array(
			'external_order_id' => $dbOrder->getId(), // used to inform a developer in case there was a problem
			'external_order_number' => $dbOrder->getNumber() // used to inform a merchant in case there was a problem
		);
	}
 
	/**
	 * Loads the products of the shop system's database and passes them to the buffer.
	 *
	 * @param int $limit pagination limit; if not null, the number of exported items must be <= $limit
	 * @param int $offset pagination; if not null, start the export with the item at position $offset
	 * @param string[] $uids a list of item UIDs that should be exported
	 *
	 * @see http://developer.shopgate.com/plugin_api/export/get_items
	 *
	 * @throws ShopgateLibraryException
	 */
	protected function createItems($limit = null, $offset = null, array $uids = array ()) {
		// This example walks through every "product" related model in the Shopgate Library,
		// showing how to put them together in order to represent complete products.
		
		// The example works with a fictional database structure and simplified functions to retrieve
		// data needed for an export.
		
		// Example: Load products for the product XML as an array, e.g. $products
		$query = 'SELECT * FROM `products`';
		
		// If $uids is set, only fetch those items referenced in $uids
		// If it's a regular call (probably an import job) exclude items depending on the setting exclude_item_ids
		if (!empty($uids)) {
			$query .= ' WHERE `product_id` IN ('.implode(',', $uids).')';
		} elseif (!empty($this->config->getExcludeItemIds())) {
			$query .= ' WHERE `product_id` NOT IN ('.implode(',', $this->config->getExcludeItemIds()).')';
		}
		
		// If $limit and $offset are set, use them to narrow your query:
		if (!is_null($limit) && !is_null($offset)) {
			$query .= ' LIMIT '.$offset.', '.$limit;
		}
		
		// Fetch products from the database with the previously built query:
		$products = db_fetch_all($query);
		
		// Create a model for each product, fill in data and add it to the output stream:
		foreach ($products as $product) {
			// Create model:
			$productModel = new Shopgate_Model_Catalog_Product();
			
			// Fill in basic data:
			$productModel->setUid($product['product_id']);
			$productModel->setName($product['name']);
			// ...
			
			// Fill in pricing data:
			$priceModel = new Shopgate_Model_Catalog_Price();
			$priceModel->setPrice($product['price']);
			$priceModel->setSalePrice($product['sale_price']);
			// ...
			
			// Add more complex pricing if necessary, e.g. tier pricing
			$tierPrices = db_fetch_all(
				'SELECT * FROM `products_tier_pricing` WHERE `product_id` = '.$product['product_id'].';'
			);
			foreach ($tierPrices as $tierPrice) {
				$tierPriceModel = new Shopgate_Model_Catalog_TierPrice();
				$tierPriceModel->setReduction($tierPrice['price_diff']);
				// ...
				
				$priceModel->addTierPriceGroup($tierPriceModel);
			}
			
			$productModel->setPrice($priceModel);
			
			// Add product image(s):
			$images = db_fetch_all('SELECT * FROM `product_images` WHERE `product_id` = '.$product['product_id'].';');
			foreach ($images as $image) {
				$imageModel = new Shopgate_Model_Media_Image();
				$imageModel->setUid($image['image_id']);
				// ...
				
				$productModel->addImage($imageModel);
			}
			
			// Set the categories the product should be shown in:
			$categories = db_fetch_categories($product['product_id']);
			foreach ($categories as $category) {
				$categoryPathModel = new Shopgate_Model_Catalog_CategoryPath();
				$categoryPathModel->setUid($category['category_id']);
				$categoryPathModel->setSortOrder($product['sort_order_by_categories'][$category['category_id']]);
				// ...
				
				$productModel->addCategoryPath($categoryPathModel);
			}
			
			// Add special shipping rules if applicable:
			if ($product['is_free_shipping']) {
				$shippingModel = new Shopgate_Model_Catalog_Shipping();
				$shippingModel->setIsFree(1);
				// ...
				
				$productModel->setShipping($shippingModel);
			}
			
			// Add extended information about the manufacturer:
			$manufacturerModel = new Shopgate_Model_Catalog_Manufacturer();
			$manufacturerModel->setTitle($product['manufacturer']);
			$manufacturerModel->setItemNumber($product['manufacturer_product_number']);
			// ...
			
			$productModel->setManufacturer($manufacturerModel);
			
			// Set the product's visibility:
			$visibilityModel = new Shopgate_Model_Catalog_Visibility();
			if ($product['hidden']) {
				$visibilityModel->setLevel(Shopgate_Model_Catalog_Visibility::DEFAULT_VISIBILITY_NOT_VISIBLE);
			} else {
				$visibilityModel->setLevel(Shopgate_Model_Catalog_Visibility::DEFAULT_VISIBILITY_CATALOG_AND_SEARCH);
			}
			// ...
			
			$productModel->setVisibility($visibilityModel);
			
			// Add the product's properties:
			$properties = $this->jsonDecode($product['properties'], true);
			foreach ($properties as $propertyName => $propertyValue) {
				$propertyModel = new Shopgate_Model_Catalog_Property();
				$propertyModel->setLabel($propertyName);
				$propertyModel->setValue($propertyValue);
				// ...
				
				$productModel->addProperty($propertyModel);
			}
			
			// Add information about how to handle stock/availability
			$stockModel = new Shopgate_Model_Catalog_Stock();
			$stockModel->setStockQuantity($product['stock']);
			// ...
			
			$productModel->setStock($stockModel);
			
			// Add product identifiers like EAN, UPC or whatever else is supported by the shopping cart:
			$identifierModel = new Shopgate_Model_Catalog_Identifier();
			$identifierModel->setType('EAN');
			$identifierModel->setValue($product['ean']);
			// ...
			
			$productModel->addIdentifier($identifierModel);
			
			// Add tags that help searching the product:
			$tags = explode(',', $product['tags']);
			foreach ($tags as $tag) {
				$tagModel = new Shopgate_Model_Catalog_Tag();
				$tagModel->setValue($tag);
				// ...
				
				$productModel->addTag($tagModel);
			}
			
			// Add related products (one model object per type, multiple models can be added):
			$relationModel = new Shopgate_Model_Catalog_Relation();
			$relationModel->setType(Shopgate_Model_Catalog_Relation::DEFAULT_RELATION_TYPE_CROSSSELL);
			$relations = db_fetch_all('SELECT * FROM `xsell` WHERE `product_id` = '.$product['product_id']);
			foreach ($relations as $relation) {
				$relationModel->addValue($relation['xsell_product_id']);
			}
			
			$productModel->addRelation($relationModel);
			
			// Add options (= variations):
			$optionCategories = db_fetch_option_categories($product['product_id']);
			foreach ($optionCategories as $optionCategory) {
				$options = db_fetch_all('SELECT * FROM `options` = '.$optionCategory['option_category_id']);
				foreach ($options as $option) {
					$optionModel = new Shopgate_Model_Catalog_Option();
					$optionModel->setUid($option['option_id']);
					// ...
					
					$productModel->addOption($optionModel);
				}
			}
			
			// Instead of options add attributes (= parent/child products) to address managing separate stock
			// levels, different images for variations etc.:
			$attributes = db_fetch_option_categories($product['product_id']);
			foreach ($attributes as $attribute) {
				$attributeGroupModel = new Shopgate_Model_Catalog_AttributeGroup();
				$attributeGroupModel->setUid($attribute['option_category_id']);
				$attributeGroupModel->setLabel($attribute['name']);
				
				$productModel->addAttributeGroup($attributeGroupModel);
			}
			
			// Add child products pointing to certain attribute groups:
			$childProducts = db_fetch_all(
				'SELECT * FROM `products` WHERE `parent_product_id` = '.$product['product_id']
			);
			foreach ($childProducts as $childProduct) {
				$childItemModel = new Shopgate_Model_Catalog_Product();
				$childItemModel->setIsChild(true);
				
				// Add attributes to the child product:
				foreach ($attributes as $attribute) {
					$option = db_fetch_all(
							'SELECT * FROM `options`'.
							' WHERE `product_id` = '.$childProduct['product_id'].
							' AND `option_category_id` = '.$attribute['option_category_id']
					);
					
					$attributeModel = new Shopgate_Model_Catalog_Attribute();
					$attributeModel->setGroupUid($attribute['option_category_id']);
					$attributeModel->setLabel($option['name']);
					$childItemModel->addAttribute($attributeModel);
				}
				
				$childItemModel->setUid($childProduct['product_id']);
				// ...
				
				// All properties not overwritten here will be copied from the parent item automatically.
				
				// To overwrite a child item's property with an empty value use the following:
				$productModel->setWeight(Shopgate_Model_Catalog_Product::SET_EMPTY);
				
				$productModel->addChild($childItemModel);
			}
			
			// Add input fields (for customizable products):
			$inputs = db_fetch_all('SELECT * FROM `input_fields` WHERE `product_id` = '.$product['product_id']);
			foreach ($inputs as $input) {
				$inputModel = new Shopgate_Model_Catalog_Input();
				$inputModel->setUid($input['input_field_id']);
				// ...
				
				$productModel->addInput($inputModel);
			}
			
			// Add the product to the export stream:
			$this->addItemModel($productModel);
		}
	}
	
	/**
	 * Loads the product categories of the shop system's database and passes them to the buffer.
	 *
	 * @param int $limit pagination limit; if not null, the number of exported categories must be <= $limit
	 * @param int $offset pagination; if not null, start the export with the categories at position $offset
	 * @param string[] $uids a list of categories UIDs that should be exported
	 *
	 * @see http://developer.shopgate.com/plugin_api/export/get_categories
	 *
	 * @throws ShopgateLibraryException
	 */
	protected function createCategories($limit = null, $offset = null, array $uids = array()) {
		// This example walks through every "category" related model in the Shopgate Library,
		// showing how to put them together in order to represent complete categories.
		
		// The example works with a fictional database structure and simplified functions to retrieve
		// data needed for an export.
		
		// Example: Load categories for the category XML as an array, e.g. $categories
		$query = 'SELECT * FROM `categories`';
		
		// If $uids is set, only fetch those items referenced in $uids
		if (!empty($uids)) {
			$query .= ' WHERE `category_id` IN ('.implode(',', $uids).')';
		}
 
		// If $limit and $offset are set, use them to narrow your query:
		if (!is_null($limit) && !is_null($offset)) {
			$query .= ' LIMIT '.$offset.', '.$limit;
		}
 
		// Fetch products from the database with the previously built query:
		$categories = db_fetch_all($query);
 
		// Create a model for each product, fill in data and add it to the output stream:
		foreach ($categories as $category) {
			// Create model:
			$categoryObj = new Shopgate_Model_Catalog_Category();
			
			// Fill in basic data:
			$categoryObj->setUid($category['category_id']);
			$categoryObj->setIsActive($category['is_active']);
			$categoryObj->setSortOrder($category['sort_order']);
 
			$categoryObj->setName($category['name']);
			
			// Set up the link to the category on the desktop website
			$categoryObj->setDeeplink('http://www.myshop.com/category/'.$category['category_id']);
			
			// Set a parent category
			if(!empty($category['parent_id'])) {
				$categoryObj->setParentUid($category['parent_id']);
			}
			
			// Load the category image for the actual category [optional]
			// -> In this sample there is an image table and an interconnecting table which sets one or more images per category. We load only the first one available here.
			$query = "SELECT `i`.* FROM `images` AS `i` INNER JOIN `categories_to_images` AS `cti` ON(`i`.`image_id` = `cti`.`image_id`) WHERE `cti`.`category_id` = {$category['category_id']}";
			$imageData = fetch_first($query);
			if(!empty($imageData)) {
				$categoryImage = new Shopgate_Model_Media_Image();
				$categoryImage->setUid($imageData['image_id']);
				$categoryImage->setSortOrder($imageData['sort_order']);
				$categoryImage->setUrl($imageData['image_url']);
				
				// Insert the image into the category [optional]
				$categoryObj->setImage($categoryImage);
			}
			
			// Insert the newly created category into the XML structure
			$this->addCategoryModel($categoryObj);
		}
	}
	
	/**
	 * Loads the product reviews of the shop system's database and passes them to the buffer.
	 *
	 * @param int      $limit  pagination limit; if not null, the number of exported reviews must be <= $limit
	 * @param int      $offset pagination; if not null, start the export with the reviews at position $offset
	 * @param string[] $uids   A list of products that should be fetched for the reviews.
	 *
	 * @see http://developer.shopgate.com/plugin_api/export/get_reviews
	 *
	 * @throws ShopgateLibraryException
	 */
	protected function createReviews($limit = null, $offset = null, array $uids = array()) {
		// Example: Load reviews for the review XML as an array, e.g. $reviews
		$query = 'SELECT * FROM `reviews`';
 
		// If $uids is set, only fetch those items referenced in $uids
		if (!empty($uids)) {
			$query .= ' WHERE `product_id` IN ('.implode(',', $uids).')';
		}
 
		// If $limit and $offset are set, use them to narrow your query:
		if (!is_null($limit) && !is_null($offset)) {
			$query .= ' LIMIT '.$offset.', '.$limit;
		}
 
		// Fetch products from the database with the previously built query:
		$reviews = db_fetch_all($query);
 
		// Create a model for each product, fill in data and add it to the output stream:
		foreach ($reviews as $review) {
			// Create model:
			$reviewObj = new Shopgate_Model_Review();
			
			// Set review data
			$reviewObj->setUid($review['review_id']);
			$reviewObj->setItemUid($review['product_id']);
			$reviewObj->setTitle($review['title']);
			$reviewObj->setText($review['text']);
			$reviewObj->setScore((int) ($review['rating'] / 2)); // convert from "1-10 rating" to "1-5 stars", depending on the system
			$reviewObj->setReviewerName($review['reviewer']);
			$reviewObj->setDate($review['date']);
			
			// Insert the review into the XML file
			$this->addReviewModel($reviewObj);
		}
	}
	
	/**
	 * Returns an array of certain settings of the shop. (Currently mainly tax settings.)
	 *
	 * @see http://developer.shopgate.com/plugin_api/system_information/get_settings
	 *
	 * @return array(
	 *		'tax' => array(
	 *			'tax_classes_products' => A list of product tax class identifiers.
	 *			'tax_classes_customers' => A list of customer tax classes.
	 *			'tax_rates' => A list of tax rates.
	 *			'tax_rules' => A list of tax rule containers.
	 *		)
	 * )
	 * @throws ShopgateLibraryException on invalid log in data or hard errors like database failure.
	 */
	public function getSettings() {
		// Database connection can be established here
		// Example: Load an array of countries with associated tax rates, e.g. $countries
		// Every country can have a sub array of provinces with additional tax rates.
 
		//initialize the result array
		$result = array(
			'tax' => array(
				'product_tax_classes' => array(
					array('key' => 'Sales Tax'),
					array('key' => 'Reduced rate'),
				),
				'customer_tax_classes' => array(
					array(
						'key' => 'Retail customer',
						'is_default' => true,
					),
					array(
						'key' => 'B2B customer',
						'is_default' => false,
					),
				),
				'tax_rates' => array(),
				'tax_rules' => array(),
			)
		);
 
		foreach ($countries as &$country) {
 
			// Use the country's tax rate to create arrays containing tax rates and a tax rules in the format as
			// specified here:
			// http://wiki.shopgate.com/Shopgate_Plugin_API_get_settings
			$taxRate = array(
				'key' => 'countryTax-' . $country['name'],
				'display_name' => 'Country Tax ' . $country['name'],
				'tax_percent' => $country['taxRate'],
				//...
			);
			$taxRule = array(
				'name' => 'State Tax ' . $country['name'],
				'tax_rates' => array(
					array('key' => 'countryTax-' . $country['name']),
				),
				'product_tax_classes' => array(
					array('key' => 'Sales Tax'),
				),
				'customer_tax_classes' => array(
					array('key' => 'Retail customer'),
				),
				'priority' => '1',
			);
 
			// Append the created tax rate and tax rule to the result array
			$result['tax']['tax_rates'][] = $taxRate;
			$result['tax']['tax_rules'][] = $taxRule;
 
			// If a country has appended provinces, create tax rates and rules for them, too...
			foreach ($country['provinces'] as $province) {
				$taxRate = array(
					//...
				);
				$taxRule = array(
					//...
				);
				$result['tax']['tax_rates'][] = $taxRate;
				$result['tax']['tax_rules'][] = $taxRule;
			}
		}
 
		return $result;
	}
 
	/**
	 * Executes a cron job with parameters.
	 *
	 * @param string $jobname The name of the job to execute.
	 * @param <string => mixed> $params Associative list of parameter names and values.
	 * @param string $message A reference to the variable the message is appended to.
	 * @param int $errorcount A reference to the error counter variable.
	 * @post $message contains a message of success or failure for the job.
	 * @post $errorcount contains the number of errors that occurred during execution.
	 */
	public function cron($jobname, $params, &$message, &$errorcount) {
		// You do not have to implement this function
		return null;
	}
 
	/**
	 * This method creates a new user account / user addresses for a customer in the shop system's database
	 *
	 * The method should not abort on soft errors like when the street or phone number of a customer is not set.
	 *
	 * @see http://developer.shopgate.com/plugin_api/customers/register_customer
	 *
	 * @param string $user The user name the customer entered at Shopgate.
	 * @param string $pass The password the customer entered at Shopgate.
	 * @param ShopgateCustomer $shopgateCustomer A ShopgateCustomer object to be added to the shop system's database.
	 * @throws ShopgateLibraryException if an error occurred
	 */
	public function registerCustomer($user, $pass, ShopgateCustomer $shopgateCustomer){
 
		if ($userNameExists) {
			throw new ShopgateLibraryException(
				ShopgateLibraryException::REGISTER_USER_ALREADY_EXISTS,
				'Username: '.$user
			);
		}
 
		$shopCustomer = new ShopCustomer();
		$shopCustomer->setEmail($user);
		$shopCustomer->setPassword(md5($pass));
 
		$shopCustomer->setFirstname($shopgateCustomer->getFirstName());
		$shopCustomer->setLastname($shopgateCustomer->getLastName());
		$shopCustomer->setGender(!strcmp($shopgateCustomer->getGender(), 'm')  ? 2 : 3);
		$shopCustomer->save();
 
		foreach($shopgateCustomer->getAddresses() as $address) {
			$shopAddress = new ShopAddress();
			$shopAddress->setFirstName($address->getFirstName());
			$shopAddress->setLastName($address->getLastName());
			$shopAddress->setStreet($address->getStreet1());
			$shopAddress->setZipcode($address->getZipcode());
			$shopAddress->setCountry($address->getCountry());
			$shopAddress->save();
		}
	}
 
	/**
	 * Exports orders from the shop system's database to Shopgate.
	 *
	 * @see http://developer.shopgate.com/plugin_api/orders/get_orders
	 *
	 * @param string $customerToken
	 * @param string $customerLanguage
	 * @param int $limit
	 * @param int $offset
	 * @param string $orderDateFrom
	 * @param string $sortOrder
	 *
	 * @return ShopgateExternalOrder[] A list of ShopgateExternalOrder objects
	 *
	 * @throws ShopgateLibraryException
	 */
	public function getOrders(
				$customerToken,
				$customerLanguage,
				$limit = 10,
				$offset = 0,
				$orderDateFrom = '',
				$sortOrder = 'created_desc'
	) {
 
		// validate customer token, e.g.:
		if (!$customerTokenIsValid) {
			throw new ShopgateLibraryException(
				ShopgateLibraryException::PLUGIN_CUSTOMER_TOKEN_INVALID,
				'token expired or invalid'
			);
		}
 
		// this result Object includes following containers => order, invoice_address, delivery_address,
		// external_coupons[], items[], delivery_notes
		
		$orders = getOrdersByToken($customerToken, $limit, $offset, $fromDate, $sortOrder);
 
		$shopgateOrders = array();
 
		foreach ($orders as $order) {
			$_tmpOrder = new ShopgateExternalOrder();
 
			$_tmpOrder->setOrderNumber($order['order_number']);
			$_tmpOrder->setIsPaid($order['is_paid']);
			// ...
 
 
			$_tmpOrder->setInvoiceAddress($order['invoice_address']);
			$_tmpOrder->setDeliveryAddress($order['delivery_address']);
			$_tmpOrder->setExternalCoupons($order['external_coupons']);
 
			$items = $order['products'];
 
 
			$shopgateItems[] = array();
			$_tmpTaxes = array();
 
			foreach ($items as $item) {
				$shopgateExternalOrderItem = new ShopgateExternalOrderItem();
				$shopgateExternalOrderItem->setItemNumber($item['article_number']);
				$shopgateExternalOrderItem->setItemNumberPublic($item['item_number_extern']);
				$shopgateExternalOrderItem->setQuantity($item['quantity']);
				// ...
 
				if (array_key_exists($item['tax_percent'], $_tmpTaxes)) {
					$item['tax_percent']['amount']++;
				} else {
					$_tmpTaxes[$item['tax_percent']] = array(
						'label' => $item['tax_percent'].' percent',
						'tax_percent' => $item['tax_percent'],
						'amount' => 1
					);
				}
 
					$shopgateItems[] = $shopgateExternalOrderItem;
			}
 
			$_tmpOrder->setItems($shopgateItems);
 
			$shopgateTaxItems = array();
			foreach ($_tmpTaxes as $_tmpTaxItem) {
				$shopgateOrderTaxItem = new ShopgateExternalOrderTax();
				$shopgateOrderTaxItem->setLabel($_tmpTaxItem['label']);
				$shopgateOrderTaxItem->setTaxPercent($_tmpTaxItem['tax']);
				$shopgateOrderTaxItem->setAmount($_tmpTaxItem['tax_amount'] );
				$shopgateTaxItems[] = $shopgateOrderTaxItem;
			}
			$_tmpOrder->setOrderTaxes($shopgateTaxItems);
 
			$_tmpExtraCosts= $order['extra_costs'];
			$shopgateExtraCosts = array();
 
			foreach ($_tmpExtraCosts as $extraCost) {
 
				switch($extraCost['type']){
					case ShopgateExternalOrderExtraCost::TYPE_SHIPPING:
						$type = 'shipping';
						break;
					case ShopgateExternalOrderExtraCost::TYPE_PAYMENT:
						$type = 'payment';
						break;
					case ShopgateExternalOrderExtraCost::TYPE_MISC:
					default:
					$type = 'misc';
					break;
 
				}
				$shopgateOrderExtraCostItem = new ShopgateExternalOrderExtraCost();
				$shopgateOrderExtraCostItem->setType($type);
				$shopgateOrderExtraCostItem->setTaxPercent($extraCost['tax']);
				$shopgateOrderExtraCostItem->setAmount($extraCost['extra_amount']);
				$shopgateExtraCosts[] = $shopgateOrderExtraCostItem;
			}
 
			$_tmpOrder->setExtraCosts($shopgateExtraCosts);
 
 
			$_tmpDeliveryNotes = $order['delivery_infos'];
			$shopgateDeliveryNotes = array();
 
			foreach($_tmpDeliveryNotes as $note){
				$shopgateDeliveryNote = new ShopgateDeliveryNote();
				// eg => ShopgateDeliveryNote::DHL
				$shopgateDeliveryNote->setShippingServiceId = $note['name'];
				$shopgateDeliveryNote->setTrackingNumber = $note['id'];
				$shopgateDeliveryNote->setShippingTime = $note['date'];
				$shopgateDeliveryNotes[] = $shopgateDeliveryNote;
			}
 
			$_tmpOrder->setDeliveryNotes($shopgateDeliveryNotes);
			$shopgateOrders[] = $_tmpOrder;
		}
 
		return $shopgateOrders;
	}
 
	/**
	 * Check items of a cart, validates stock quantity of the products and returns available amount.
	 *
	 * @see http://developer.shopgate.com/plugin_api/stock
	 *
	 * @param ShopgateCart $cart The ShopgateCart object to be checked and validated.
	 * @return ShopgateCartItem[], # list of cartItems with validated stock
	 *
	 * @throws ShopgateLibraryException if an error occurs.
	 */
	public function checkStock(ShopgateCart $shopgateCart) {
		// Database connection can be established here
 
		// Create a cart in your shopping system solution
		$shopCart = new ShopCart();
 
		$validatedItems = array();
		foreach ($shopgateCart->getItems() as $item) {
			try {
				/* @var $item ShopgateOrderItem */
				$shopCartItem = $shopCart->addItem(array(
													'article_number' => $item->getItemNumber(),
													'article_name' => $item->getName(),
													// ...
				));
 
				// create a ShopgateCartItem from the ShopgateOrderItem
				$cartItem = new ShopgateCartItem($item->toArray());
 
				// set isBuyable and actual stock quantity
				$cartItem->setIsBuyable(true);
				$cartItem->setStockQuantity($shopCartItem->getQty());
								// ...
			} catch (Exception $e) {
 
				$cartItem->setIsBuyable(false);
				$cartItem->setErrorText($e->getMessage());
			}
 
			$validatedItems[] = $cartItem;
		}
 
		return $validatedItems;
	}
 
	/**
	 * Updates and returns synchronization information for the favourite list of a customer.
	 *
	 * @see http://developer.shopgate.com/plugin_api/customers/sync_favourite_list
	 *
	 * @param string $customerToken
	 * @param ShopgateSyncItem[] $items A list of ShopgateSyncItem objects that need to be synchronized
	 *
	 * @return ShopgateSyncItem[] The updated list of ShopgateSyncItem objects
	 */
	public function syncFavouriteList($customerToken, $items) {
		// Database connection can be established here.
		// Check if the user's customer token exists in the shop
		// If user data is available, save them in, for instance, the $dbCustomerData array.
		
		if ($customerNotFoundByToken) {
			throw new ShopgateLibraryException(ShopgateLibraryException::PLUGIN_CUSTOMER_TOKEN_INVALID);
		}
		
		// Fetch the current favourite list into $dbFavouriteList
		// ...
		
		// Walk through the list passed by Shopgate and update the local list
		foreach ($items as $item) {
			/* @var $item ShopgateSyncItem */
			
			$index = array_search($item->getItemNumber(), $dbFavouriteList);
			switch ($item->getStatus()) {
				case 'new':
					if ($index === false) {
						$dbFavouriteList[] = $item->getItemNumber();
					}
				break;
				case 'deleted':
					if ($index !== false) {
						unset($dbFavouriteList[$index]);
					}
				break;
			}
		}
		
		// Save the updated list to the database
		// ...
		
		// Create the list to be returned to Shopgate
		$newFavouriteList = array();
		foreach ($dbFavouriteList as $itemNumber) {
			$newFavouriteList[] = new ShopgateSyncItem(array('item_number' => $itemNumber));
		}
		
		// Return the new favourite list
		return $newFavouriteList;
	}
}
 ```
