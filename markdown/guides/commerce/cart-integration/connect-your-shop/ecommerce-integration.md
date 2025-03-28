---
stoplight-id: tng2lfg3xsabp
---

# Checklist: Integrate an E-Commerce Plattform
Please be aware that Shopgate APIs and imports are designed for fair usage. Please use the API responsibly and avoid sending excessive or repetitive requests that could be avoided. We reserve the right to limit or suspend access if unintended usage effects our service for others.   

If you're looking for a guidance which way you should use to i.e. implement the export, please contact our support.

## Minimum Requirements

In order to allow your customers to browse and buy products inside the app, these steps need to be completed:


**Categories are shown in the app.**

Ways of implementation:

Export of XML: **LINK** 
Full Feature Set, full files only, one file per local, import max. once per hour

Export of JSON: **LINK**  
Full Feature Set, full & delta files, content localization in one file, real-time-updates possible

Export of CSV: **LINK**  
Limited Feature Set, see documentation for details

Real-time-Updates: **LINK**  
Requires JSON export as full import


**Products are shown in the app.**

Ways of implementation:

Export of XML: **LINK** 
Full Feature Set, full files only, one file per local, import max. once per hour

Export of JSON: **LINK**  
Full Feature Set, full & delta files, content localization in one file, real-time-updates possible

Export of CSV: **LINK**  
Limited Feature Set, see documentation for details

Real-time-Updates: **LINK**  
Requires JSON export as full import

**Basic Web-Checkout Integration**
Cart and user handling as well as checkout redirect is implemented
**LINK** ../../webcheckout/overview.md

**Order and Customer endpoint**
Add endpoints that provide required information for Shopgate to update the app dashboard  
**TBD**


## Best App Experience

Our goal is to provide your customers the best possible app experience. Therefore we strongly recommend implementing these features.

**Product reviews are available in the app**
Ways of implementation
**Manual export of XML:** Product reviews XML format  
(Full Feature Set, full files only, one file per local, import max. once per hour)*

**Third Party Review Source:** Extension  
(In case your reviews are managed by an external source, you can either check for available integrations with our support team, your review source or implement your own extension by overriding/extending the review pipelines shopgate-reviews-pipelines.oas2.yml or load external content inside the app.)

**Favorite List Sync**. 
Allow your customers favorite list(s) to be in sync with your ecommerce platform. Otherwise they are saved only in the Shopgate system.  
**TBD**

**Profile Pages / Order History etc.**  
Open user profile pages in webshop  
**LINK**  

or  

[Build native profile pages inside the app  ](../../../../tutorials/advanced/ecp-integration.md)

**Allow app only offers**
Allow your marketing users to create app only offers like coupons
**LINK**



## Code Examples

**Webcheckout**. 

You can look up our Shopware 6 Webcheckout integration as an example:  
Endpoints on shop-side: https://github.com/shopgate/shopware6-webcheckout  
Utilities Extension: tbd  
User Extension: tbd  
Cart Extension: tbd  
Favorites Extension  
Web-Account Extension: tbd