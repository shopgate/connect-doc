---
title: App Architecture
stoplight-id: fr7rfyqnd8hna
---
# App Architecture


 An application built on the Shopgate CONNECT platform is
 a progressive web app (PWA) with a UI based on React
 that runs inside a native wrapper app. Native wrappers
 are available for iOS and Android so you can easily
 distribute your app on the Apple App Store or Google
 Play.


 Shopgate provides ready-to-run default themes (the React
 app) for e-commerce applications. You can modify themes
 with Shopgate portals, or you can create custom themes
 that can be modified or completely replaced by custom
 themes. 

 The app frontend is based on JavaScript, and the
 frontend communicates to the native wrapper app through
 a system of commands and events. 


 The wrapper app displays a single full-screen web view,
 which is a browser window without any controls. The
 wrapper app loads the frontend of your app into the
 single full-screen web view.


!["App Architecture"](../../../assets/app-architecture.png)


To communicate with the native parts of the app, a
 JavaScript library is injected into the web view. This
 library is connected to a native library contained in
 the app’s native code. By calling app commands and
 listening to events, the frontend can access native
 functionality, such as camera, brightness, and
 vibration, and can talk to native SDKs and frameworks.


 Both the app frontend and native wrapper also connect to
 the backend infrastructure. The backend is based on
 micro-service architecture.

>**Next:**
>
>[Infrastructure Overview](infrastructure-overview.md)
