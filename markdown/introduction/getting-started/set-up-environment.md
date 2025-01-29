# Set up Your Developer Environment


 ## Prerequisites


 Before you start with Shopgate CONNECT, make sure you
 have **created a Developer Account**. Then, install the
 following software on your machine:


 * [Node.js](https://nodejs.org/) (Version 8.4 or higher)
 * [Git](https://git-scm.com/)


 Shopgate also recommends basic knowledge of the
 following tools and technologies:


 * [Node.js](https://nodejs.org/) (for backend development), [Tutorial on w3schools.com](https://www.w3schools.com/nodejs/nodejs_get_started.asp)
 * [React](https://reactjs.org/) (for frontend development), [Tutorial on egghead.io](https://egghead.io/courses/start-learning-react)
 * [Redux](https://redux.js.org/) (optional, for data handling), [Tutorial on egghead.io](https://egghead.io/courses/getting-started-with-redux)


 ## Install the Shopgate CONNECT Platform SDK


 The Shopgate CONNECT Platform SDK is based on
 [Node.js](https://nodejs.org/). The Shopgate CONNECT
 Platform SDK requires Node.js version 8.4 or later
 installed on your developer machine.


 1. Open a terminal as a user with permission to install
 software.
 2. Type `npm install -g @shopgate/platform-sdk` in the
 terminal.


 >**Note:** 
 >
 >Due to the large number of node modules and their
 >dynamic development, you may see error or warning
 >messages from time to time, such as peer dependencies,
 >that most likely will not affect your work with the SDK.
 >Continue and if you have an issue, contact [Shopgate
 >Support](/support/contact).*


 Now you have the `sgconnect` command available on the
 command line to perform all actions required to develop
 and test your extensions.


 ## Connect Your Local Development Environment with Your Developer Account
 


 1. Type `sgconnect login`
 2. Enter the email address and password that you set up
 during registration. Now you are logged in on this
 machine.


 ## Install a REST client (optional)


 To develop extensions for the backend, such as adding
 steps to pipelines or defining new pipelines, Shopgate
 recommends installing a REST client. Shopgate recommends
 the [Postman](https://www.getpostman.com/) client, but
 you can use any tool that can request a REST API
 endpoint. You do not need a REST client to only make
 changes to the theme.


 ## Start with a Sandbox


 You can use Sandbox apps as a testing environment to
 build your themes or extensions.


 ## Starting a New Project


 1. Create a new empty folder.
 2. Open a terminal and run: `sgconnect init` This
 command creates all subfolders and files required to
 develop for the specified sandbox app within your
 project folder.
 3. Enter the sandbox application ID. You can find your
 application IDs in Developer Center. 


 If you only want to develop server-based code (pipeline
 steps) and create or modify pipeline configurations,
 this is all you need to set up locally.


>**Next:**
>
> [Set Up Local Frontend](set-up-local-frontend.md)
