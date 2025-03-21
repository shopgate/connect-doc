## Steps to integrate


 Follow these steps sequentially to implement the Web Checkout. 


 ### Step 1 - Web Checkout API


 #### Step 1.1 - Authentication


 As mentioned in "Authentication", you must
 implement a route to authenticate Shopgate Connect with
 the shop system. To use Basic Authentication,
 you just have to secure your server.


 In case of OAuth2, the Web Checkout API needs to accept
 the grant type
 [client_credentials](https://tools.ietf.org/html/rfc6749#section-1.3.4)
 and return an access token on `POST /oauth/token`. All
 of the following routes need the access token for
 authentication.


 #### Step 1.2 - Cart


 Implement the following cart routes in your shop system:


 - [**Create cart**](web-checkout-apis.oas2.yml/paths/~1carts/post)
 `POST /carts`
 Creates a new cart within the shop system and returns its ID. This ID is used for both an anonymous cart and a user cart.

 - [**Get cart**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}/get)
 `GET /carts/{cartId}`
 Returns the given cart, including all items such as products and coupons. All price calculations take place here.

 - [**Adding product(s) to the cart**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}~1products/post)
 `POST /carts/{cartId}/products`
 Adds one or more products to the cart. Keep in mind, adding the same product multiple times does not create multiple new cart items, but rather increases cart item quantity.

 - [**Adding coupon(s) to the cart**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}~1coupons/post)
 `POST /carts/{cartId}/coupons`
 Adds one or many coupons to the cart and validates these coupons.

 - [**Update quantity of product(s) within the cart**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}~1cartItems~1{cartItemId}/patch)
 `PATCH /carts/{cartId}/cartItems/{cartItemId}`
 Updates product quantity in the cart. Decreasing product quanitity to zero removes the product from the cart.

 - [**Remove cart items from the cart**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}~1cartItems~1{cartItemId}/delete)
 `DELETE /carts/{cartId}/cartItems/{cartItemId}`
 Removes an item from the cart entirely.
 
 These routes are independent of the user and can
 be tested without having the user routes implemented.


 #### Step 1.3 - User


 Implement the following user-related routes in your shop
 system.


 - [**Login user**](web-checkout-apis.oas2.yml/paths/~1login/post)
 `POST /login`
 Returns the internal user ID used for the calls of all the other user-related requests.
 
 - [**Get user**](web-checkout-apis.oas2.yml/paths/~1users~1{userId}/get)
 `GET /users/{userId}`
 Returns the basic user info such as name, addresses, etc.
 
 
 - [**Get current cart id of user**](web-checkout-apis.oas2.yml/paths/~1users~1{userId}~1cartId/get)
 `GET /users/{userId}/cartId`
 Returns the given user's cart ID.
 
 
 - [**Merge cart with user cart**](web-checkout-apis.oas2.yml/paths/~1users~1{userId}~1mergeCart~1{cartId}/post)
 `POST /users/{userId}/mergeCart/{cartId}`
 Merges a cart with the current user cart. The relation of user and user cart is held within the shop system. The non user-related cart and the cart attached by the user are merged.
 

 #### Step 1.4 - Checkout


 - [**Get checkout url**](web-checkout-apis.oas2.yml/paths/~1carts~1{cartId}~1checkoutUrl/post)
 `POST /carts/{cartId}/checkoutUrl`
 This URL leads the user to the app-ready checkout page of the shopping system. When a user is logged in, the response also contains a token that logs the user into the shop system for the checkout process.
 
 The issued token is valid only once and also expires within a short timespan, like one minute.
 

 ### Step 2 - Navigation to the checkout


 Once you create the route for fetching the checkout URL,
 the user can now enter the checkout.


 #### Step 2.1 Remove all links


 In the checkout, you must remove links to other pages
 (like start page, product detail page, or other internal
 pages) to keep the shopper in the app. Pages like terms &
 condition should be handled as popups or a page without
 links.



 #### Step 2.2 - Send tracking event


 After the checkout succeeds, you must send a
 tracking event to the native tracker.


 The app offers a JavaScript handler that sends the
 event to the native part.


 To call this handler, include the following script in
 the head tag of the page:

 ```

 <script src="https://data.shopgate.com/webcheckout/generic/commandLib.v1.js"></script>

 ```


 After you include the JS library, you have access to the
 `window.SGAction` object.


 Calling the function
 `window.SGAction.sendCheckoutSuccessEvent(params)` with
 the params shown in the example below triggers the
 tracking event.


 Example:

```javascript=
var params = {
    order: {
        number: '1234789', //order number as a string
        currency: 'EUR', //Currency of the order. Format: ISO 217
        totals: [ // all (sub)sums of the order
            {
                type: 'shipping',
                amount: 5.00, // shipping total as a float
            },
            {
                type: 'tax',
                amount: 53.2
            },
            {
                type: 'grandTotal',
                amount: 1222
            }
        ],
        products: [
            {
                id: 'SG40', //id of the product
                name: 'Some awesome product',
                quantity: 1,
                price: {
                    withTax: 280.00,
                    net: 226.8
                }
            }
        ]
    }
};


document.addEventListener("DOMContentLoaded", function () {
    window.SGAction.sendCheckoutSuccessEvent(params);
});

```

>**Note:** 
>
> Ensure that all prices are passed as floating numbers and the order number as string.

#### Step 2.3 - Close checkout on success

 Depending on the theme of the shop system, the checkout
 success page contains a button like `Continue Shopping`,
 which brings the user back to the start page.


 In the webcheckout, the user needs to leave the checkout view to return to the main view.


 The JS library (which was included in Step 2.2) includes
 a function to close the checkout via one function call:


 ```javascript=
$('#continueButton').click(function () {
    window.SGAction.closeInAppBrowser();
});
 ```


 After this function is called, the user returns to
 the apps start screen.

 The same applies for pressing the `Close` button at the
 top right corner.


 ### Step 3 - Registration


 #### Step 3.1 - Open registration

 To open the registration, configure the shop system 
 registration URL in the [Shopgate
 Merchant Admin](https://admin.shopgate.com).


 After this is done, the user opens the registration
 from the shop system.


 > **Note:** 
 >
 > All links that lead to other pages must be removed on the registration page. 


#### Step 3.2 - Log in user after registration


 When the user opens a successful registration from the app, you must send the
 credentials to the app.


 To do so, create a page with just a loading spinner. From
 this page, you can send the successful registration event to the app.


 To trigger the event, you must integrate the following
 script into the `head` tag of your application.

 ```htmlmixed=
 <script src="https://data.shopgate.com/webcheckout/generic/commandLib.v1.js"></script>
 ```


 After this script loads, call the
 following:


 ```javascript=
 document.addEventListener("DOMContentLoaded", function () {
    window.SGAction.userDidRegister(email, password);
});
 ```
