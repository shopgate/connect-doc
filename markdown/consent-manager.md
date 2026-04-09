---
stoplight-id: 3npp9umgibvh5
---

# Shopgate Consent Manager 

## How to Evaluate if User Accepted Cookie Consent
This guide provides instructions on how to evaluate whether a user has accepted cookie
consent (both comfort and statistics cookies) in a React-Redux-based application. The code
below shows how you can connect to the Redux store and access the necessary state to check
the user's cookie preferences. 

### Overview
To evaluate the user's cookie consent preferences, you need to check the state of specific
cookies: *comfort* cookies and *statistics* cookies. This is done by connecting a React component to the Redux store, retrieving the current cookie consent status, and making use of specific selectors.

### Code Example
#### Connecting Redux to Component
You can connect the required state to your component using react-redux's connect
function. This will allow you to access the cookie consent state (comfort and statistics cookies)
from the Redux store.

```js
import { connect } from 'react-redux';
import {
  getAreComfortCookiesAccepted,
  getAreStatisticsCookiesAccepted,
} from '@shopgate/engage/tracking/selectors';

/**
* @return {Object} The extended component props.
*/


const mapStateToProps = (state) => ({
  comfortCookiesAcceptedState:getAreComfortCookiesAccepted(state),
  statisticsCookiesAcceptedState:getAreStatisticsCookiesAccepted(state),
});
export default connect(mapStateToProps);
```

#### Explanation of the Code
- *mapStateToProps* Function:
  - This function is used to map the Redux state to the component's props.
  - *getAreComfortCookiesAccepted* and *getAreStatisticsCookiesAccepted* are used to get the current status of the user’s consent for comfort and statistics cookies respectively.
- *connect*:
  - The *connect* function from *react-redux* connects the *mapStateToProps* to the component, enabling it to read from the Redux store and dispatch actions.

#### How to Use This in Your Component
Once the Redux state is connected, you can access the cookie consent status and use it within
your component. Below is an example of how to use the previously created connector.js:

```js
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import connect from './connector';
/**
* Your component
*/
class YourComponent extends Component {
  render() {

  const {
    comfortCookiesAcceptedState,
    statisticsCookiesAcceptedState,
  } = this.props;
  return (
    //...your code
  );
  }
}
YourComponent.propTypes = {
  comfortCookiesAcceptedState: PropTypes.bool.isRequired,
  statisticsCookiesAcceptedState: PropTypes.bool.isRequired,
};
export default connect(YourComponent);
```
### Key Points
- Comfort Cookies: These typically include non-essential cookies that improve user experience (e.g., for personalization).
- Statistics Cookies: These are used to collect data for analytics purposes (e.g., to track user behavior on the site).

### Conclusion
This approach helps you evaluate the cookie consent status in a React-Redux application by
connecting your component to the Redux store. By using the provided selectors, you can easily
retrieve the user's cookie consent preferences.
