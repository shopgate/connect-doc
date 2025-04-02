# Category XML

## Sample File for Categories

You can download a sample file [here](http://files.shopgate.com/xml/example/category_example.xml).

Additionally the XSD file to validate can be found [here](http://files.shopgate.com/xml/xsd/catalog/categories.xsd).

## Fields

If any node is missing, the file cannot be imported. If the value in a row is invalid, the category cannot be imported.

Generally, the more information we receive, the better the categories can be displayed in our mobile shop, and the higher the conversion rate. If the value of an allowed empty column is invalid, it will be ignored, but the category will still be imported.

> **⚠ Important:** The file encoding must be UTF-8!

| Node | Attributes | Allow empty | Description | Example |
| --- | --- | --- | --- | --- |
| category Shopgate_Model_Catalog_Category | uid<br>sort_order<br>is_active<br>parent_uid | ✕<br>✔<br>✔<br>✔ | Unique ID<br><br>Sort-order; highest value displayed first<br><br>Is active (0 or omitted means inactive)<br><br>Parent Category UID (must be omitted for top-level categories) | 5<br>1<br>1<br>1 |
| name STRING |  | ✕ | Category name | Living Room |
| deeplink STRING |  | ✕ | Link to the category | http://shop.com/living-room |
| image Shopgate_Model_Media_Image | uid | ✔ | Unique ID | 5 |
| url STRING |  | ✕ | Image Url Note: If the tag is empty the importer won't break, but then the image tag is useless | http://shop.com/media/living-room.jpg |

## Caption

| Field/Key | Icon | Description |
| --- | --- | --- |
|  | ✕ | Field is required |
|  | ✔ | Field is not required |
|  | ⚑ | Field requirement depends on other values or fields Please read the description of the field for more information |
| _value |  | The value of the node itself |