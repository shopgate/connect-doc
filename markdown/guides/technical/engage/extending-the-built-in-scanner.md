# Extending the built-in Scanner

The Engage app has a built-in scanner functionality. The scanner recognizes QR codes and barcodes of different [formats](#supported-scanner-formats). The core implementation performs a product search for scanned barcodes and can handle QR codes created within the Shopgate merchant admin.

This guide shows you how to open the scanner, implement custom handling of scanned data, change the appearance of the default scanner page, and create a completely custom scanner route.

## Table of Contents

- [Opening the Scanner](#opening-the-scanner)
- [Custom Handling of Scan Results](#custom-handling-of-scan-results)
- [Modifying the Default Scanner Route](#modifying-the-default-scanner-route)
- [Creating a Custom Scanner Route](#creating-a-custom-scanner-route)
- [Supported Scanner Formats](#supported-scanner-formats)

## Opening the Scanner

The default scanner is available at the route `/scanner`. As you can see in the following table, the route accepts two query parameters, which activate different modes. When the scanner is opened without any parameters, defaults apply.

| Name | Supported Values | Default |
| - | - | - |
| `type` | `barcodeRecognition` | `barcodeRecognition` |
| `scope` | any URL safe string | `default` |

The parameter `type` specifies the recognition mode of the scanner. Currently, only `barcodeRecognition` is supported, which activates the barcode / QR code mode, but there are more types to come. The parameter `scope` is used to implement custom handling for scanned data. It can be set to any URL safe value.

Let's create a React component that provides a link to open the barcode scanner in a custom scope.

```javascript
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { getScannerRoute } from '@shopgate/engage/scanner';

const MyCustomScannerLink = () => (
  <Link href={getScannerRoute('myScope')}>Open My Custom Scanner</Link>
);

export default MyCustomScannerLink;
```

Notice that we use the `getScannerRoute` helper function from `@shopgate/engage/scanner` to generate a link to the scanner page. This link opens the default scanner page with activated barcode scanner mode. Additionally, it sets a custom `scope`, which deactivates the default scan result handling of the PWA core. We can then implement custom handling of the scan results.

> The helper accepts a `type` as second parameter, but since currently only one scanner type is supported, in can be kept empty and returns to `barcodeRecognition`.

## Custom Handling of Scan Results

When the scanner recognizes barcodes or QR codes, predefined streams emit. You can use these streams to implement custom handling for scanned data.

For an introduction to streams and how you can use them within your extension, refer to the Shopgate [Streams Guide](/guides/technical/engage/streams). To learn more about available scanner streams, refer to the Shopgate [Scanner Reference](/references/engage/streams/scanner).

The following snippet implements basic handling for incoming scanner data of our just opened scanner route.

```javascript
import { historyReplace } from '@shopgate/engage/core';
import { scannerFinishedBarCode$, startScanner } from '@shopgate/engage/scanner';
import processScanData from './processScanData';

const scannerFinishedBarCodeMyScope$ = scannerFinishedBarCode$.filter(({ action }) => {
  const { scope } = action;
  return scope === 'myScope';
});

subscribe(scannerFinishedBarCodeMyScope$, async ({ dispatch, action }) => {
  const { format, payload } = action;

  const success = await processScanData(format, payload);

  if (success) {
    // Remove the scanner route after successful processing of the scanner payload.
    dispatch(historyReplace({
      pathname: '/scan-results',
    }));
  } else {
    // Restart the scanner, so that the user can retry scanning.
    dispatch(startScanner());
  }
});
```

For this example, we assume that we only want to handle barcodes. Therefore, we create a local stream that filters the `scannerFinishedBarCode$` stream from the Engage core by our custom scope.

When the new stream emits, the scanned data is processed. If the scan is successful, the user is redirected to a new page that displays the scan results. The example utilizes `historyReplace` for the redirect, so that the browsing history of the user is not interrupted on back navigation. However, any other history action can be used.

Immediately after a scan occurs, further image recognition stops. This prevents additional incoming scan events caused by a barcode that is still within the camera focus. If the scan does not process successfully, the scanner restarts by dispatching `startScanner` to give the user another opportunity for a successful scan.

### Example of the Action Object from the Stream

```json
{
   format: "EAN_13",
   payload: "8540660239843",
   scope: "customScope",
   type: "SCANNER_FINISHED"
}
```

| Key | Description |
| - | - |
| `format`| Format of the scanned data. See available formats [here](#supported-scanner-formats). |
| `payload`| Payload of the scanned barcode or QR code. |
| `scope`| Scope of the scanner event. |
| `type`| Type of the Redux action. |

## Modifying the Default Scanner Route

There are multiple [Portals](/guides/technical/engage/portals) you can use to modify the default scanner route. Refer to the Shopgate [Scanner Reference](/references/engage/portals/scanner) for a complete list.

In the following snippet, we change the appearance of the camera overlay when the scanner opens in our custom scope.

```javascript
import React from 'react';
import { useRoute } from '@shopgate/engage/core';
import MyCameraOverlay from '../MyCameraOverlay';

const ScannerCameraPortal = ({ children }) => {
  const { query: { scope } } = useRoute();

  if (scope !== 'myScope') {
    // Render the original portal content when the scope differs from "myScope".
    return children;
  }

  return (
    <MyCameraOverlay />
  );
}

export default ScannerCameraPortal;
```

Returning `children` at other scopes ensures that our extension does not interfere with the default PWA scanner. The component would be registered for the `scanner.camera` portal position, which wraps the built-in camera overlay.

## Creating a Custom Scanner Route

You can also provide a custom scanner route within your extension. For an introduction to implementing custom routes, please refer to the Shopgate [Guide to Creating Custom Routes](/guides/technical/engage/creating-custom-routes).

As you can see in the following code example, a component for a custom scanner route does not differ much from common custom routes. 

```javascript
import React from 'react';
import { useTheme } from '@shopgate/engage/core';
import { SCANNER_TYPE_BARCODE } from '@shopgate/engage/scanner';
import { Route, ScannerContainer } from '@shopgate/engage/components';
import MyCameraOverlay from '../MyCameraOverlay';

const MyScannerRoute = () => {
  const { View, AppBar } = useTheme();

  return (
    <View background="transparent">
      <AppBar title="Custom Scanner Page" />
      <ScannerContainer scope="myScope" type={SCANNER_TYPE_BARCODE}>
        <MyCameraOverlay />
      </ScannerContainer>
    </View>
  );
};

export default () => (
  <Route pattern="/my_scanner" component={MyScannerRoute} />
);
```

You just need to ensure that the `background` prop for the `View` is set to "transparent" to make the camera feed visible underneath the page content.

By wrapping the page content with the `<ScannerContainer />` component from `@shopgate/engage/components`, the actual scanner is initialized with `scope` and `type`. Listening to scanner events works as described in the previous sections.

## Supported Scanner Formats

- AZTEC
- CODE_39
- CODE_93
- CODE_128
- DATA_MATRIX
- EAN_13
- EAN_8
- ITF
- PDF_417
- UPC_E
- QR_CODE