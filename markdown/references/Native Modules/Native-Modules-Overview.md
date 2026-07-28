---
stoplight-id: bqzh3fhyknb42
---

# Native Modules

`@shopgate/native-modules` is the library that gives the app's web layer access to
native device and platform capabilities — camera, push, geolocation, secure storage,
analytics SDKs, and system UI. Each capability is exposed as its own module with a
small, promise-based API, so the web code can call native functionality as if it were
a normal async function.

```jsx
import { Camera, Push, Geolocation } from '@shopgate/native-modules';
```

This document is the entry point. Every module has its own reference page (linked
below) with a full API description and copy-paste React examples.

## How the modules work

A few conventions apply across all modules:

- **Promise-based.** Every method returns a `Promise`. Call them from React event
  handlers or effects with `async/await`.
- **Import per module.** Import only what you need from `@shopgate/native-modules`.
  Each module is a named export (`Camera`, `Push`, `StatusBar`, …).
- **Events.** Modules that push state to the web layer expose
  `addEventListener(name, handler)` / `removeEventListener(name, handler)`. Register
  in a `useEffect` and clean up on unmount. Examples: connectivity changes, incoming
  push, deep links, in-app-browser open/close, Braze card updates.
- **Platform differences.** Some methods are platform-specific. Android-only calls
  (e.g. the Android navigation bar) resolve to `undefined` on iOS; a few options are
  iOS- or Android-only and are marked as such on the module page.
- **Real-device features.** Camera, brightness, and similar hardware features require
  a real device — simulator behaviour may differ.

## Modules by area

### Device & hardware

| Module | Purpose | Docs |
|--------|---------|------|
| Camera | Native scanner, flashlight, and base64 JPEG image capture. | [Camera.md](./Camera.md) |
| Brightness | Read and set the screen brightness (0–100%). | [Brightness.md](./Brightness.md) |
| Geolocation | Configure location services, request authorization, read current position. | [Geolocation.md](./Geolocation.md) |
| Connectivity Monitor | Report online/offline state and connection type (WIFI/2G/3G/4G), with a change event. | [ConnectivityMonitor.md](./ConnectivityMonitor.md) |

### System UI

| Module | Purpose | Docs |
|--------|---------|------|
| Status Bar | Control status-bar color, style, visibility, and translucency. | [StatusBar.md](./StatusBar.md) |
| Android Navigation Bar | Control the Android system navigation bar; report gesture-nav and dark-mode state (Android only). | [AndroidNavigationBar.md](./AndroidNavigationBar.md) |
| Splash Screen | Show or hide the native launch splash screen. | [SplashScreen.md](./SplashScreen.md) |
| In-App Browser | Open external and SG API pages in native browser views and control their navigation bars. | [InAppBrowser.md](./InAppBrowser.md) |

### Navigation, sharing & networking

| Module | Purpose | Docs |
|--------|---------|------|
| Linking | Open a URL outside the app; listen for universal and deep links. | [Linking.md](./Linking.md) |
| Sharing | Open the platform share sheet with a message and optional URL/title. | [Sharing.md](./Sharing.md) |
| HTTP | Perform native HTTP requests with optional cookie synchronization. | [Http.md](./Http.md) |

### Permissions & security

| Module | Purpose | Docs |
|--------|---------|------|
| App Permissions | Check and request runtime permissions (camera, location, push, ATT). | [AppPermissions.md](./AppPermissions.md) |
| Keychain | Securely store and retrieve a username/password pair on the device. | [Keychain.md](./Keychain.md) |

### Push & messaging

| Module | Purpose | Docs |
|--------|---------|------|
| Push | Check notification permission and retrieve the device push token; `pushReceived` event. | [Push.md](./Push.md) |

### Analytics & engagement SDKs

| Module | Purpose | Docs |
|--------|---------|------|
| Braze | User identity, custom events, purchases, content cards, banners, push permission, user attributes. | [Braze.md](./Braze.md) |
| Emarsys | Predict recommendations and commerce tracking. | [Emarsys.md](./Emarsys.md) |
| Firebase Analytics | Standard ecommerce/engagement events, consent, user IDs and properties. | [FirebaseAnalytics.md](./FirebaseAnalytics.md) |
| Facebook Analytics | App events, purchases, push-open tracking, consent, user identity. | [FacebookAnalytics.md](./FacebookAnalytics.md) |

## Quick example

```jsx
import { useEffect, useState } from 'react';
import { ConnectivityMonitor } from '@shopgate/native-modules';

export function ConnectionStatus() {
  const [state, setState] = useState(null);

  useEffect(() => {
    const handleChange = (event) => setState(event.detail);
    ConnectivityMonitor.addEventListener('onConnectivityStateChange', handleChange);
    ConnectivityMonitor.getCurrentConnectivityState().then(setState);

    return () => {
      ConnectivityMonitor.removeEventListener('onConnectivityStateChange', handleChange);
    };
  }, []);

  return <p>{state ? `${state.type}: ${state.connected ? 'online' : 'offline'}` : 'Loading…'}</p>;
}
```

See each module's page for its full API and more examples.
