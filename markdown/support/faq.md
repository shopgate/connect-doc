# FAQ


## How do I get the current product ID and price in the event that gets triggered on the PDP page? I need to call an API with the data at this point.

`productWillEnter$` is not enough for this because at the time this stream emits, the product data might not yet be there.

Try this stream instead: `receivedVisibleProduct$` https://github.com/shopgate/pwa/blob/adb8fac6e49a039cf8f7670de8f313c9dffabd89/libraries/commerce/product/streams/index.js#L70

`action.productData` should have all the data you need.


## When a customer opens a particular category and a list of products appear, how do I retrieve a specific piece of data from all the products under that category? 

https://github.com/shopgate/pwa/blob/ce1a8ba54ad4deba1289c7868c64aa09f5a89cda/libraries/tracking/streams/category.js#L44



## How can I get the Shopgate connect full URL?

You cannot, because the URL changes with every deployment.

## How do I link to the Category or Item page with an ID?

Use the <Link> component + bin2hex(ID).

## How do I get the Product/Cateogry ID from a URL?

Use `hex2bin(IdFromUrl)`.

## How can I hide/show the TabBar from iOS Theme?

import { withThemeComponents } from '@shopgate-ps/pwa-extension-kit/connectors'

withThemeComponents(yourComponent)  → will provide TabBar as a prop to your component.

TabBar.hide() / TabBar.show()


## How can I get the device ID?

In a backend step, the device ID can be obtained with `context.app.getInfo()`

https://developer.shopgate.com/references/connect/extensions/steps/app-info


## Which of my extension components need to be identified in the extension configuration?

Portals, Translations, Reducers, and Subscribers (a.k.a Subscriptions) all need to be identified in the extension-config.json file in the components array. 

Example portal component configuration:
````

{
  "id": "TabBarBrowse",
  "path": "frontend/portals/TabBar/TabBarBrowse/index.jsx",
  "target": "tab-bar.browse",
  "type": "portals"
}
````
Example translation component configuration:
````
{
  "type": "translations",
  "path": "frontend/locale/en-US.json",
  "id": "locale/en-US"
}
````
Example reducer component configuration:
````
{
  "id": "extensionReducer",
  "path": "frontend/reducers/index.js",
  "type": "reducers"
}
````
Example subscriber (subscription) component configuration:
````
{
  "id": "subscriptions",
  "path": "frontend/subscriptions/index.js",
  "type": "subscribers"
}
````
## Where does my extension's reducer add its data to the redux store?

The reducers of all extensions add data to the 'extensions' property of the redux store. The property name of the extension object to which the extension's reducer saves its data is a combination of the extension's ID and the specific reducer's ID, which is defined in the extension-config.json file. For example, if your extension has the ID '@my-organization/cool_extension', and your reducer has the ID 'extensionReducer', the data would be stored at state.extensions["@my-organization/cool_extension/extensionReducer"].



## How can I make my extension accommodate multiple languages?

1) Start by creating locale files. These files are JSON files that are given names that correspond to the language/country for the language they contain. For instance, the file that contains translations for English US would be called 'en-US.json'.  It is best to scope your extension-specific translations with something unique to your extension. This scoping is important because the locale files of your extension, all other extensions, and the theme are combined. If you do not scope your translation information, your translations may overwrite that of the theme or other extensions, or may be be overwritten by translations from another extension.

Example locale file:

````
{
  "mySpecialExtension": {
    "form": {
      "title": "Newsletter Signup Form"
    }
}
````

2) Identify the translation files in your extension extension-config.json file. Each translation file (you will have one for every language you support) needs to be identified separately as a component in the extension configuration.

Example configuration:
````
"components": [
{
  "type": "translations",
  "path": "frontend/locale/en-US.json",
  "id": "locale/en-US"
},
{
  "type": "translations",
  "path": "frontend/locale/de-DE.json",
  "id": "locale/de-DE"
}
]
````

3) To use one of your translations, you can employ the `I18n` React component, provided by the @shopgate/pwa-common library.
Import this component as follows:
import I18n from '@shopgate/pwa-common/components/I18n';

Then, use the component like this:
````
const FormWrapper = props => (
  <div>
    <h1>
      <I18n.Text string="mySpecialExtension.form.title" />
    </h1>
    <MyForm />
 </div>
);
````

## How can I create a new page (custom route) in the app?

Follow this guide to create a new page or a custom route in the app: 
[Creating Custom Routes](markdown/guides/technical/engange/creating-custom-routes.md)

## Can I access the checkout or registration pages when viewing the app content in a browser?

No. When the user progresses to the checkout or registration page he/she is redirected to web content that is external to the app. This is one of the reasons the Engage app is so flexible. It can redirect users to external content but display that content within an independent web view inside of the app. The router used by the React portion of the Engage app is able to determine if the path passed to it is external and, if it is, it can trigger the native app to open a new web view to display that content. However, this is not possible when viewing the React portion of the app within a browser, as is done during the development process, because there is no native app to open a new web view.  Using an external checkout source allows the Engage app to integrate easily with multiple checkout services, including the mobile website's checkout or the Shopgate checkout. The checkout process can be tested using the Shopgate CloudFlight app. There is a version available for Android and iOS devices. 



## Can I access the checkout and registration pages when viewing the app in CloudFront app and running the code in the local SDK?

Yes. When using the CloudFront testing app you are able to access the registration page and checkout pages of the app. The content of these pages are hosted externally to the app so the app will open that external content in an independent web view. However, when using the Shopgate legacy checkout and legacy user, you must have the Shopgate legacy user extension checked out locally and attached to the SDK when running your code.



## How can I access Theme components?

You can access theme components by importing the Theme context from the @shopgate/engage/core library. The Theme context is a React component that can function as a child. This function receives the theme components as props, and then you can utilize the component(s) you like within that function.

Example with `ProductSlider` component:

Import Theme from library:
````
import { Theme } from '@shopgate/engage/core';
Access and use ProductSlider component:

<Theme>
  {({ ProductSlider }) => (
    <ProductSlider
      autoplay
      delay={7000}
      productIds={['123', '456']}
      slidesPerView={2.3}
      snap={false}
    />
  )}
</Theme>
````
Using the PWA Extension Kit provided by the Shopgate Professional services team makes this process even easier. See the documentation here: https://github.com/shopgate-professional-services/pwa-extension-kit/blob/master/src/connectors/README.md#withThemeComponents.

## How do I call a custom pipeline from the frontend?

Most of the time you will call a pipeline from within an action. The shopgate pwa-core library provides a class called `PipelineRequest` that makes calling pipelines easy.

Import `PipelineRequest` like this:

import PipelineRequest from '@shopgate/pwa-core/classes/PipelineRequest';
Pass the `PipelineRequest` constructor with the value of the ID of your custom pipeline, excluding the version. For example if the ID of the pipeline you would like to call is "myOrganization.myExtension.getLoyaltyPoints.v1" you would pass the PipelineRequest constructor "myOrganization.myExtension.getLoyaltyPoints". If your pipeline requires an input, for example a product ID,  use the `setInput` method of `PipelineRequest` to do this. Pass an object to the `setInput` method containing the input. For instance, if the custom pipeline expected an input called "productId" you would pass the `setInput` method, something like `{ productId: '123' }`.

Using `PipelineRequest` to make a pipeline call might look something like this:
````
export const fetchLoyaltyPoints = productNumber => (dispatch) => {
  dispatch(requestLoyaltyPoints(productNumber));

  new PipelineRequest('myOrganization.myExtension.getLoyaltyPoints')
   .setInput({
   productNumber,
    })
   .dispatch()
   .then((response) => {
      const { loyaltyPoints } = response;
      dispatch(receiveLoyaltyPoints(productNumber, loyaltyPoints));
    })
   .catch((err) => {
      logger.error(err);
      dispatch(errorLoyaltyPoints(productNumber));
   });
};
````

## How can I call an action when a user enters a specific page/route of the app?

Though there is more than one approach that could be employed to achieve this outcome, most of the time it is best to use a subscription. The Shopgate app uses a system of streams and subscriptions. A stream is like an event, and a subscription (sometimes called subscriber) is like an event handler. This system makes it easy to create new streams by manipulating existing ones. To create a stream that triggers when entering a specific route or page of the app, you would filter the `routeDidEnter$` stream provided by the Shopgate pwa-common library. Remember to register your subscription in the extension-config.json file in the components array.

Import the `rourteDidEnter$` stream like this:

import { routeDidEnter$ } from '@shopgate/pwa-common/streams/router';
Create your custom stream by from the routeDidEnter$ stream by the filter method of that stream. The filter method takes a function as a parameter. When that function returns true your new stream is triggered.

Your custom streams would look something like:
````
const didEnterMyCustomRoute$ = routeDidEnter$.filter(({ action }) => (
  action.route.pathname ==='/my-custom-route'
));
Your subscription would look something like:

const enterMyRouteSubscriptions = (subscribe) => {
  subscribe(didEnterMyCustomRoute$, ({ dispatch }) => {
    dispatch(customRouteAction());
  });
};
````
## How can I set a constant that holds information that may be different for each merchant, like an API key that can be easily configured?

The Connect system allows you to create configurations that can be set easily in the admin. Here is information on creating configurations for your extension: https://developer.shopgate.com/references/connect/extensions/configuration.

## How do I add data to the redux store?

You need to create a reducer to add data to the redux store. The reducer is registered in the extension-config.json file. The reducer is a function. When it is registered, it passes every action object that is created. It is typical to use a switch to check the action type and take appropriate action when the action type has a specific value. Here is more information about reducers: https://redux.js.org/basics/reducers.


## Can the backend of the extension store information, like a cart token, for later use?

Yes. Here is information on backend storage: https://developer.shopgate.com/references/connect/extensions/steps/storage.

