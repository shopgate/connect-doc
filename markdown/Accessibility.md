---
stoplight-id: jxjykma5naa67
---

# Accessibility

As of June 28, 2025, the [European Accessibility Act (EAA)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32019L0882) will be fully enforced and aims to make products and services accessible to people with disabilities, including websites and apps. Businesses in the European Union need to ensure equal access of consumers to their products by meeting specific accessibility standards. The same applies to the [Americans with Disabilities Act (ADA)](https://www.ada.gov/) which is already in place.

Therefore, we strive to keep our components up to date and accessible in all use cases. This includes testing the app by navigating it with a screen reader on different devices - VoiceOver on iOS and TalkBack on Android.

When implementing new code or refactoring the existing code base, please make sure to adhere to the [fundamentals](https://www.w3.org/WAI/fundamentals/accessibility-intro/) recommended by the Web Accessibility Initiative.

For example, this means favouring native html elements whenever possible, e.g. using button, input, and a tags for links instead of giving custom styling and functionality to a div or a span. Moreover, images should have either a descriptive alt-text to be announced by the screen reader or should be hidden from screen readers if they are purely decoration.

Also, pay attention to a sufficient colour contrast and font-size of the elements on your page. This isn't just important for individuals with visual disabilities but it is in fact user-friendly for all customers.

### Reduce Motion Hook

Shopgate offers a hook to detect reduce motion settings by users. This hook should be used in order to reduce motion/animations: [Hook](https://docs.shopgate.com/docs/connect-doc/fiswddb89tznw-hooks#usereducemotion)
