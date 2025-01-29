# Cloud Flight

For universal testing, Shopgate provides Cloud Flight, an app available for iOS and Android in the app stores.

You can use this app to test the applications associated with your developer or merchant account from within our native app framework. Testing is very important if you use native app commands or events in your developed extensions. Testing also gives you the chance to have the on-device experience that shoppers will have when you deploy the application to the live shop. 

To use Cloud Flight, complete the following steps:

## 1. Install Cloud Flight to your mobile device.

* For iOS, install [Cloud Flight for iOS](https://itunes.apple.com/us/app/cloud-flight/id1334710652) from the Apple App Store.
* For Android, install [Cloud Flight for Android](https://play.google.com/store/apps/details?id=com.shopgate.uta) from the Google Play Store.

## 2. Add your developer account.

Complete these steps to add your developer account:

1. Open the Cloud Flight app. 
2. Click **Add developer account** on iOS or **Action** on Android.
3. Enter the same credentials that you use for Shopgate Developer Center. Click **Login**.

Your developer account is now authenticated and will be stored on the device for two months. Anyone with access to the device has access to your sandbox applications. 

You can add multiple developer accounts to the same device. If your email address is linked to a Gravatar account, the app will display your image, name, and email address on the account list view.

In Cloud Flight version 1.1 and later, you can add merchant accounts using the same process to access staging and live applications.

## 3. Select the application and theme to use.

To start testing an application, tap an account on the account list view to see a list of connected applications grouped by the developer organizations they belong to. Tap on the application you want to test and select from these two options:

**Themes: Default**  

In this mode, the app loads the deployed theme of the application same way as the regular native app framework does. If necessary, ensure that no SDK is connected to this sandbox application.

**SDK: Use local theme**  

In this mode, the app attempts to connect to your locally running webpack instance on your development computer. Your SDK must be connected to this sandbox application and your local frontend must be running. Also the Cloud Flight device must be in the same local network as your development computer. The app detects the IP address to connect to because the SDK sends this information to the Shopgate backend.

## 4. Start your test flight

When you select the application and theme to use, a summary of your configuration is shown. To start your test flight, tap Take off. Cloud Flight enters flight mode, and the app frontend is loaded in the same way as the native app framework. You can now start testing your app. All native app commands and events are available in this mode.

>**Note:**
>
> Native modules and SDKs that are activated by adding some configuration, such as an API 
> key, to the apps Plist (iOS) or Manifest (Android) will not work. To test these kinds of 
> feature, use the merchant preview apps instead.

## 5. End your test flight or start over.

While the app is in flight mode, it behaves like the standard native app framework used for live applications. If you close the app or it crashes and you
start it again, the previously selected app frontend is started again.

To end your test flight, turn your device upside down. A service menu appears where you can tap End flight to return to the Cloud Flight main menu. On iOS the app terminates and you have to re-launch it.
