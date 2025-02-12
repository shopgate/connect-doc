---
stoplight-id: jnc3wmecn79ek
---

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