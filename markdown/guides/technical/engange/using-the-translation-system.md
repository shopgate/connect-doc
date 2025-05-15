# Using Translations
The Shopgate platform provides translation support that enhances the theme and extension development experience. This article explains how the translation process works and how to use it.

## Introduction to Using Translations
Every Shopgate theme provides its own locales dictionary. You can find them in our [Github repository](https://github.com/shopgate/pwa/tree/master/themes/theme-ios11/locale).

Bookmark these links in case you need them later. Please note that the above examples are for theme-iOS. For theme-GMD, please see the [this github repository directory](https://github.com/shopgate/pwa/tree/master/themes/theme-gmd/locale).

During app start up, the theme checks if there are any locales provided by extensions, selects relevant ones (according to the shop language settings), merges them with defaults provided by the theme itself, and then uses it as a source for [`i18n helper`](../../../references/engage/helpers/i18n.md) and [`I18n Component`](../../../references/engage/components/i18n.md).

This construction empowers you as an extension developer to not only __provide your custom translation__ strings, but also to __override default translations__ provided by the theme. Please note that overriding default translations affects the entire application.

## How to Use Translation Support
The Shopgate system provides two ways of using translations:

### [i18n helper](../../../references/engage/helpers/i18n.md)
The `i18n helper` is a set of pure javascript translating functions. Use it when you need to translate text outside of the `React` context.
[Read i18n helper documentation](../../../references/engage/helpers/i18n.md)

### [I18n component](../../../references/engage/components/i18n.md)
The `I18n component` is a set of `React Components` made for translations within the `React` context.
[Read I18n component documentation](../../../references/engage/components/i18n.md)

## How to Use Custom Extension Locales
If your extension provides a UI to the end customer, you most likely need to translate your content into the customer language.

If you do not find any relevant default translations provided by the theme you need to provide you own translations within an extension.

### 1. Creating Translations
Create your locale files in any `frontend` directory. For example: `frontend/locales/en-US.json`. This is a pure JSON file which has a structure like this:

```json
{
  "myExtensionName": {
    "myTranslationString": "Human readable, translated text"
  }
}
```

Please note that the translation file starts with `myExtensionName`. It is a good practice to namespace your translations in order to avoid possible conflicts with default translations. It is possible to intentionally create these conflicts in order to override theme translations. 

### 2. Declaring Your Translation in the Extension-config
When you have your translation files in place, you only need to declare them in the `extension-config.json` file, like in the example below:
```json
{
  "version": "1.0.0",
  "id": "@exampleOrg/exampleExtensionName",
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
}
```

### 3. Testing Your Translation

You are nearly finished. The final step is to test if your translation works by implementing it in your UI, using either [i18n helper](../../../references/engage/helpers/i18n.md) or [I18n component](../../../references/engage/components/i18n.md).