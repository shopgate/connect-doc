# Using Translations

Shopgate Engage provides translation support that enhances the theme and extension development experience. 

This article explains how the translation process works and how to use it.

## Introduction to Using Translations
Every Shopgate theme provides its own locales dictionary. You can find an [en-US locales example of theme-ios11 on Shopgate's Engage github repository](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/en-US.json).

At the moment (v6.7.0) all our themes provide these languages out of the box:
- [de-DE - German](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/de-DE.json)
- [en-US - English (US)](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/en-US.json)
- [es-ES - Spanish](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/es-ES.json)
- [fr-FR - French](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/fr-FR.json)
- [it-IT - Italian](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/it-IT.json)
- [nl-NL - Dutch](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/nl-NL.json)
- [pt-PT Portuguese](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-ios11/locale/pt-PT.json)

Bookmark these links in case you need them later. Please note that the above examples are for theme-ioS11. For theme-GMD, please see the [relevant github repository directory](https://github.com/shopgate/pwa/blob/v6.7.0/themes/theme-gmd/locale).

During app start up, the theme checks if there are any locales provided by extensions, selects relevant ones (according to the shop language settings), merges them with defaults provided by the theme itself, and then uses it as a source for [`i18n helper`](/references/engage/helpers/i18n) and [`I18n Component`](/references/engage/components/i18n).

This construction empowers you as an extension developer to not only __provide your custom translation__ strings, but also to __override default translations__ provided by the theme.

__It is however NOT RECOMMENDED__ to override default translations and doing so must be agreed upon. Please note that overriding default translations affects the entire application and causes additional issues for future updates.

## How to Use Translation Support
Shopgate Engage provides two ways of using translations:

### [i18n helper](/references/engage/helpers/i18n) (since 6.7.0)
The `i18n helper` is a set of pure javascript translating functions. Use it when you need to translate text outside of the `React` context.
[Read i18n helper documentation](/references/engage/helpers/i18n)

### [I18n component](/references/engage/components/i18n)
The `I18n component` is a set of `React Components` made for translations within the `React` context.
[Read I18n component documentation](/references/engage/components/i18n)

## How to Use Custom Extension Locales
If your extension provides a UI to the end customer, you most likely need to translate your content into the customer language.

If you do not find any relevant default translations [provided by the theme](#how-it-works) you need to provide you own translations within an extension.

### 1. Creating Translations
Create your locale files in any `frontend` directory. For example: `frontend/locales/en-US.json`. This is a pure JSON file which has a structure like this:

```json
{
  "myExtensionName": {
    "myTranslationString": "Human readable, translated text"
  }
}
```

Please note that the translation file starts with `myExtensionName`. It is a good practice to namespace your translations in order to avoid possible conflicts with default translations.

It is possible to intentionally create these conflicts in order to override theme translations. But as stated before, we highly discourage this approach.

### 2. Declaring Your Translation in the Extension-config
Now, when you have your translation files in place, you only need to declare them in the `extension-config.json` file, like in the example below:
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

You are nearly finished. The final step is to test if your translation works by implementing it in your UI, using either [i18n helper](/references/engage/helpers/i18n) or [`I18n component`](/references/engage/components/i18n).


## More Information
For more information and specific details on how to use our translation system please refer to:
- [I18n Component](/references/engage/components/i18n)
- [i18n helper](/references/engage/helpers/i18n)
