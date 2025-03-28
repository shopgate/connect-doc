---
stoplight-id: tng2lfg3xsabp
---

# Integrate E-Commerce Plattform

## Minimum Requirements

In order to allow your customers to browse and buy products, these steps need to be completed:

1. Categories are exported to Shopgate.
> **Ways of implementation**
> 
> 
> **Export of XML:** Categories XML format  
> *(Full Feature Set, full files only, one file per local, import max. once per hour)*
> 
> **Export of JSON:** Categories JSON format  
> *(Full Feature Set, full & delta files, content localization in one file, real-time-updates possible)*
> 
> **Export of CSV:** Categories CSV format  
> *(Limited Feature Set, see documentation for details)*
> 
> **Real-time-Updates:** JSON format  
> *(Requires JSON export as base)*


2. Products are exported to Shopgate (Milestone [Export products](#export-of-products)).
> **Ways of implementation**
> 
> **Export of XML:** Products XML format  
> *(Full Feature Set, full files only, one file per local, import max. once per hour)*
> 
> **Export of JSON:** Products JSON format  
> *(Full Feature Set, full & delta files, content localization in one file, real-time-updates possible)*
> 
> **Export of CSV:** Products CSV format  
> *(Limited Feature Set, see documentation for details)*
> 
> **Real-time-Updates:** JSON format  
> *(Requires JSON export as base)*

3. Basic Web-Checkout with cart and user handling as well as checkout redirect is implemented
../../webcheckout/overview.md

4. Endpoint for Shopgate order dashboard import is provided 
**TBD**


## Best App Experience

Our goal is to provide your customers the best possible app experience. Therefore we strongly recommend implementing these features.

1. Product reviews are available in the app.
> **Ways of implementation**
> 
> **Manual export of XML:** Product reviews XML format  
> *(Full Feature Set, full files only, one file per local, import max. once per hour)*
> 
> **Third Party Review Source:** Extension  
> *(In case your reviews are managed by an external source, you can either check for available integrations with our support team, your review source or implement your own extension by overriding/extending the review pipelines shopgate-reviews-pipelines.oas2.yml or load external content inside the app.)*

2. Favorite List Sync
**TBD**

3. Open user profile pages in webshop / build native profile pages
../../../../tutorials/advanced/ecp-integration.md

4. Allow app only offers
**TBD**



## Code Examples

- **Webcheckout**
You can look up our Shopware 6 Webcheckout integration as an example:
Endpoints on shop-side: https://github.com/shopgate/shopware6-webcheckout
Utilities Extension: tbd
User Extension: tbd
Cart Extension: tbd
Favorites Extension
Web-Account Extension: tbd