---
stoplight-id: 9rev43erlubny
---

# Scanner Streams

* [scannerDidEnter$](#scannerdidenter)
* [scannerFinished$](#scannerfinished)
* [scannerFinishedBarCode$](#scannerfinishedbarcode)
* [scannerFinishedQrCode$](#scannerfinishedqrcode)

## scannerDidEnter$

Triggers when the default scanner's route is entered.

### Usage

```javascript
import { scannerDidEnter$ } from '@shopgate/engage/scanner';

subscribe(scannerDidEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

---

## scannerFinished$

Triggers when the scanner finishes scanning something.

### Usage

```javascript
import { scannerFinished$ } from '@shopgate/engage/scanner';

subscribe(scannerFinished$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

---

## scannerFinishedBarCode$

Triggers when the scanner completes a barcode scan.

### Usage

```javascript
import { scannerFinishedBarCode$ } from '@shopgate/engage/scanner';

subscribe(scannerFinishedBarCode$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

---

## scannerFinishedQrCode$

Triggers when the scanner completes a QR code scan.

### Usage

```javascript
import { scannerFinishedQrCode$ } from '@shopgate/engage/scanner';

subscribe(scannerFinishedQrCode$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```