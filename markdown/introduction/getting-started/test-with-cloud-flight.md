---
title: Test With Cloud Flight
---
# When to choose Cloud Flight over the desktop browser

 While you can test most of your application in the
 browser, there are certain cases where the native
 wrapper app is required. You need the native wrapper app
 when you have app commands that invoke native
 functionality, such as camera and vibration. You also
 need the native wrapper app when you are handling events
 coming from the device, such as orientation and
 gyroscope.


# Usage of the Cloud Flight testing app

 To test these features without deploying your
 code over and over again, Shopgate provides the Cloud
 Flight app. Cloud Flight is a native testing app for both
 iOS and Android devices. You can log in with the
 credentials of your developer account and easily access
 all your sandbox applications from within a single
 native app. It can also connect to your local webpack
 instance of the Platform SDK to test a local theme.

 Cloud Flight is available in the Apple App Store or in
 Google Play. Download and install Cloud Flight on your
 test devices and log in with your developer account.


* [Cloud Flight for iOS](https://itunes.apple.com/us/app/cloud-flight/id1334710652)
* [Cloud Flight for Android](https://play.google.com/store/apps/details?id=com.shopgate.uta)


# Development and testing with Engage

## Registration and checkout

 The Engage app consists of two subsystems. The first one is
 the GMD and IOS11 themes and the second is the classic system.
 Some shops do not use the classic system for user handling and
 checkouts and instead use Web-Checkout.

 Every subsystem works as a unit in its own tab window, within
 the app. The connection and data transfer between the subsystems is handled
 via the app; it accepts app commands and sends events between the
 tabs. This process enables different tabs to communicate with each other.
 Therefore, the app is required whenever subsystems need
 to share information with one another. For example,
 when the Engage theme tries to open the registration or checkout
 page and sends data back when it is closed.

 Testing this process in a desktop browser would be unsuccessful because only
 a native app can share data between different tabs (or windows); the desktop browser simply
 ignores the command to navigate to a different tab.
 Whenever an app command is dispatched in a desktop browser window,
 there will be some log output to the console to inform the developer of
 what the application just tried to do. There will be no error shown in
 this case, which is desired behavior.

## Testing Web-Checkouts

 Many shops are set up to use the Web-Checkout instead of the
 classic Shopgate system to handle the user login and registration
 functionality, as well as to perform the checkout itself.
 The same principle applies for these shops, with one difference.

 The shops come with at least
 two additional extensions for Web-Checkout to work. The first is a trusted extension
 for user handling and synchronizing between the original desktop
 shop and the Engage app. The second is a cart
 extension, which takes Engage actions like "addProductToCart" and
 places the product in the user's cart in the original shop, rather
 than within the Shopgate infrastructure. The product usually still
 comes from the data sources of the Shopgate classic system, but 
 can be sourced from the original shop with
 further customization, if necessary.
 
 These extensions are mostly backend extensions, but come with a small
 frontend layer that handles opening the original shop's registration
 and checkout pages. This means to test everything in full, you must attach all involved extensions before any testing can be done.
 The Shopgate Platform SDK comes with a handy command to attach multiple
 extensions at once:
 * `sgconnect extension manage`
 * Scroll through the list, check all extensions to attach using the
   space key, and confirm with the enter key.

 The testing can only be done within the Cloud Flight app, as described
 above, or by using the shop preview app, which can be found in
 the Merchant admin area. The preview app requires the shop to be deployed
 with all extensions in order to test everything together.
 For the development process, it is easier to work with the Cloud Flight app.
