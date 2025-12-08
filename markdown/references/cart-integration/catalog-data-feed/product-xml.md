# Product XML

## Sample File for Products

You can download a sample file [here](http://files.shopgate.com/xml/example/items_example.xml).

## Fields

If any of the nodes are missing, the file cannot be imported. An exception to that rule are child products. A missing node in a child product will result in the property being derived from the parent product. An empty node in a child product on the other hand will overwrite the property with an empty value.

If the value in a node that doesn't allow empty values is invalid, the product cannot be imported. However, an invalid value in an "allow empty" field is ignored and the product will still be imported.

Generally, the more information we receive, the better the product can be displayed in our mobile shop, and the higher the conversion rate.

> **⚠ Important:** File encoding must be UTF-8!

| Node | Type | Attributes | Allow empty | Description | Example |
| --- | --- | --- | --- | --- | --- |
| item Shopgate_Model_Catalog_Product | String | uid | ✕ | Unique ID Note: Every item needs a unique item number (uid). If items have identical item numbers, they cannot be imported to Shopgate. | 5 |
| name | String |  | ✕ | Product name | Example Product |
| tax_percent | Float |  | ⚑ | Tax percent -maximum of two decimal places -no percentage symbol Attention: Use this field only if your system does not support tax classes. For tax class support use tax_class. | 19 |
| tax_class | String |  | ⚑ | Tax class Identifier of a tax class in your store. The main identifier is the name or ID of the tax class. The name should be the same as the defined in tax settings. Attention: Use this field only if your system supports tax classes. To export gross amounts use tax_percent. | 19% DE |
| currency | String |  | ✕ | Currency ISO 4217 currency code (EUR, CHF, USD). | EUR |
| description | String |  | ✔ | Product description Note: Enter an item description. Please use HTML formatting. | With your high-resolution micro-speakers that deliver full-range audio, the ergonomic ... |
| deeplink | String |  | ✔ | Deeplink Link to the items detail page Complete link to the item in your shop. This information enables to link items in the app with your shop site. | http://shop.com/ipod-touch-32gb.html |
| internal_order_info | String |  | ✔ | Internal order info In this field you can store additional information that will automatically be sent to you with any order. This information will not be visible to the customer. | ..... |
| weight | Float | unit | ✔ | set the weight (units g, lb, kg and oz). Default g | 25 |
| prices Shopgate_Model_Catalog_Price | | type | ✔ | set the price type (net / gross) if nothing is set, gross is default | gross |
| price | Float |  | ⚑ | This price is the basic price without any discounts. If price is not set sale_price needs to be set. | 19.99 |
| sale_price | Float |  | ⚑ | This price is the price a customer has to pay (e.g. with discounts). If sales_price is not set price needs to be set. If sale_price is cheaper than price, price becomes the 'was price' and sale_price will be used as item price. | 15.99 |
| cost | Float |  | ✔ | This is the price a merchant has to pay (purchase price). | 11.21 |
| msrp | Float |  | ✔ | Manufacturer’s suggested retail price. Default 0 positive value maximum of two decimal places no currency symbol | 22.00 |
| minimum_order_amount | Float |  | ✔ | Minimum order amount. Default 0 (For example: Product price is 1 cent but only if you your order is at least $50) | 25.00 |
| base_price | String |  | ✔ | The base price is a price per unit. This value needs to be set e.g. for food. | 10.00 € / kg |
| tier_prices | Array |  | ✔ | set the tier price items |  |
| tier_price Shopgate_Model_Catalog_TierPrice | | threshold<br>max_quantity<br>type<br>customer_group_uid | ✕<br>✔<br>✕<br>✔ | threshold ( > 0)<br>maximum quantity<br>type (percent, fixed)<br>customer group id | 10<br>5<br>percent<br>1 |
| _value | Float |  | ✕ | value for the tier price. Fixed discount or percentage discount. Relative to the item's price (sale_price if cheaper than price) | 12.00 |
| images | Array |  | ✔ | set the images items |  |
| image Shopgate_Model_Media_Image| | sort_order | ✔ | sort order of the image; smallest value displayed first | 2 |
| url | String | | | ✕ | Image Url | http://shop.com/media/hello.jpg |
| categories | Array |  | ✕ | set the categories items |  |
| category Shopgate_Model_Catalog_CategoryPath | | uid<br>sort_order | ✕<br>✔ | set the uid sort order of the product inside the category;<br>highest value displayed first |  |
| shipping Shopgate_Model_Catalog_Shipping | |  | ✔ | Shipping costs for the product if specific ones exist. |  |
| costs_per_order| Float |  | ✔ | costs per order The highest value in costs_per_order of an item in the cart is added once to the regular shipping costs during checkout. positive value maximum two decimal places no currency symbol Default 0 | 5.99 |
| additional_costs_per_unit | Float |  | ✔ | additional costs per unit Additional shipping costs per unit. This value is added to the shipping costs of the order. positive value maximum two decimal places no currency symbol Default 0 | 2.99 |
| is_free | Bool |  | ✔ | is free shipping If this field is set to "1", the customer will not have to pay for any shipping costs. Attention: If the cart contains an item with "additional_costs_per_unit," the shipping of this item will also be free. Default 0 | 0 |
| manufacturer Shopgate_Model_Catalog_Manufacturer | |  | ✕ | Set manufacturer details |  |
| title | String |  | ✔ | set the manufacturer name | Apple |
| item_number | String |  | ✔ | external item number | apple_123 |
| visibility Shopgate_Model_Catalog_Visibility | | level | ✔| nothing: item will not be visible while browsing the app. The product can only be accessed with a direct link, or by searching for the exact article - number. <br><br>0: Item will be shown in the app | nothing |
| properties | Array |  | ✔ |  |  |
| property Shopgate_Model_Catalog_Property ||| uid | ✔ | Property UID. If no ID provided the property cannot be used for sorting / filter. | 463 |
| label | String |  | ✕ | Label of the property | Megapixels |
| value | String |  | ✕ | Value could also contain HTML | 8 |
| stock Shopgate_Model_Catalog_Stock| |  | ✕ |  |  |
| is_saleable | Bool |  | ✔ | 1 if the product is saleable. Default 0 | 1 |
| use_stock | Bool |  | ✔ | Product uses stock? Default 0 (no inventory management) | 1 |
| stock_quantity | Int |  | ✔ | Stock quantity. Default 0 | 5 |
| minimum_order_quantity | Int |  | ✔ | The minimum order quantity that must be ordered at least. | 1 |
| maximum_order_quantity | Int |  | ✔ | The maximum order quantity that can be ordered. | 500 |
| availability_text | String |  | ✔ | Availability text | 2-3 business |
| identifiers| Array |  | ✔ |  |  |
| identifier Shopgate_Model_Catalog_Identifier | | uid<br>type | ✕<br>✕ | uid<br>if needed types: ean, ean13, sku, upc, pzn or isbn | 10<br>ean |
| _value | String |  |  |  | 12345678 |
| tags | Array |  | ✔ | Tags are indexed, which allows searching for products by tags. |  |
| tag Shopgate_Model_Catalog_Tag | |  | ✕ | Product Tag | car |
| relations | Array |  | ✔ |  |  |
| relation Shopgate_Model_Catalog_Relation | | type | ✕ | Indicate additional relations to the product upsell crosssell/crossell bonus ordered_with custom | upsell |
| uid | String |  | ✕ | Product ID for the relation | 122 |
| label | String |  | ⚑ | Required if type = custom | users_also_buy |
| attribute_groups parent product only |Array |  | ✔ |  |  |
| attribute_group Shopgate_Model_Catalog_AttributeGroup | | uid | ✕ | attribute group id | 80 |
| inputs | Array |  | ✔ |  |  |
| input Shopgate_Model_Catalog_Input | |uid<br>type<br>sort_order<br>additional_price<br>price_type<br>required | ✕<br>✕<br>✔<br>⚑<br>⚑<br>✔ | input id<br><br>type (see possible types below) input<br><br>sort order (see below) for text and image types only and required<br><br>price type (fixed or percentage, not for select type)<br><br>required or not | 3<br>text<br>1<br>4.99<br>fixed<br>1 |
| label | String |  | ✕ | Label for the input | PC Tower case color |
| info_text | String |  | ✔ | Info text shown in a question mark | The tower color will be specially made for you |
| options | Array |  | ✔ |  |  |
| option Shopgate_Model_Catalog_Option | | uid<br>additional_price<br>price_type<br>sort_order | ✔<br>✔<br>✔<br>✔ | option id additional price for the option price type (fixed, percentage) sort order (lowest first) | 3 0.99 fixed 1 |
| label | String |  | ✕ | Option Label | Color |
| display_type parent product only | |  | ✔ | display type explanation can be seen below. | list |
| children Shopgate_Model_Catalog_Product | |  |  | Make sure this node is the last node for every item. In general node order is not important, but it is important that the "children" node is the last node for each item. children have got the same nodes as their parent product except for display_type attribute_groups (instead of attribute_groups they have attributes) inheritance rules if a tag is missing at the child, the child will have the according value from its parent any tag present at the child will override the value from their parents especially: if a tag is present but empty the value from the parent will not be used (the value becomes empty) |  |
| attributes | Array | group_uid | ✕ | refers to the uid of the corresponding attribute_group at parent product | 80 |

# Details for Product Export

## Input Types

- text
- select

## Input Sort Order

If sort_order attribute is given inputs will be displayed on the page in this order. Lowest value first. If sort order is missing the sequence in the xml file will be used instead.

**Note:** at the moment it is not possible to mix input fields with select boxes. Select boxes will always be displayed first on the page.

## Display Type

- default
- simple
- select
- list: The display type is a special form of displaying products in relations like parent child. For example: You sell a t-shirt in different colors and sizes. Therefore you need a select field with color and one with size. Display type will be "select" If you sell a the black one in S on a special deal for example, it gets default display type to be able to show in the drop down as option and as single product. The System decides which will be the correct way up on request
If you sell a couch, for example, with options to order several pieces from the middle, corners and so on, display type would be list. This way the user is able to set different amounts for sub products on a single page and put them all directly in the cart.

## Customer Group for Tier prices

To use tier prices, you need to export the customer groups in get_settings. Each customer group needs to have unique ID and a name as well as a default flag ( 0 or 1) and a tax class.