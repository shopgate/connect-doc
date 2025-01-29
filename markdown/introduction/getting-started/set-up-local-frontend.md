---
title: Set Up Local Frontend
---
# Set Up Local Frontend


 ## Add a Theme to Your Project


 To test your frontend locally, you need to have a
 Shopgate theme in your project. You can either create a
 theme or check out one of our ready-to-go themes from
 GitHub.


 ## Using the Default Android Theme


 ```shell
 $ cd themes
 $ git clone https://github.com/shopgate/theme-gmd.git
 $ cd theme-gmd
 $ npm i
 $ cd ../..
 ```


 ## Set Up the Frontend Environment


 Type `sgconnect frontend setup` to set up the local
 frontend environment. For most cases, you can accept the
 default values for all requested settings. For more
 information, refer to the [Platform SDK
 guide](/guides/tools/platform-sdk).


 You only need to run the setup step once for every
 project folder. Later you can omit it.


 ## Start the Frontend Environment


 1. Type `sgconnect frontend start` to start the frontend
 environment.
 2. Wait until the integrated Webpack process compiles
 your theme sources and starts the local development
 server. 
 3. After the compile process finishes, you can access
 the locally running application by opening the
 development server URL in your browser: 
 `http://{YOUR_LOCAL_IP_ADDRESS}:{PORT}`


 You should see your application frontend.


 *Note: The port is set to 8080 by default. If you
 changed the port during setup, you need to use the new
 port to access the development server URL.*


>**Next:**
>
> [Test with Cloud Flight](test-with-cloud-flight.md)  
or continue with our [Kick-start Tutorials](/tutorials)
