# Review XML

## Sample File for Reviews

You can download a sample file [here](http://files.shopgate.com/xml/example/reviews_example.xml).
Additionally the XSD file to validate can be found [here](http://files.shopgate.com/xml/xsd/catalog/reviews.xsd).

## Fields

If any of the nodes is missing, the file cannot be imported. If the value in a node is invalid, the review cannot be imported.

Generally, the more information we receive, the better the reviews can be displayed in our mobile shop, and the higher the conversion rate. If the value of an allowed empty node is invalid, it will be ignored, but the review will still be imported.

> **⚠ Important:** File encoding must be UTF-8!

| Node | Attributes | Allow empty | Description | Example |
| --- | --- | --- | --- | --- |
| review Shopgate_Model_Review | uid | ✕ | Unique ID | 5 |
| item_uid  | STRING | ✕ | Product / Item UID | 36 |
| score  | INT | ✕ | Score value (0 - 10) | 4 |
| reviewer_name  | STRING | ✔ | Username or Display-name of the review author | Natashenka |
| date  | DATE | ✕ | Created at | 2007-08-25 |
| title  |  STRING| ✔ | Review title | Chicks dig ribs |
| text  | STRING | ✔ | Review text | Ever since buying this shirt chics cant take their hands off me. I don't know what it is it must be... |