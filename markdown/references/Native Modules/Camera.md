---
stoplight-id: irb3pvbg7ithl
---

# Camera Module

The Camera module controls the native scanner and flashlight and captures base64-encoded JPEG images. Camera operations require a real device; simulator behavior may vary by platform.

```jsx
import { Camera } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useState } from 'react';
import { Camera } from '@shopgate/native-modules';

export function CameraControls() {
  const [image, setImage] = useState(null);

  const captureImage = async () => {
    try {
      await Camera.openScanner();
      const result = await Camera.captureImage(300);
      setImage(`data:image/${result.format};base64,${result.imageData}`);
    } finally {
      await Camera.closeScanner();
    }
  };

  return (
    <div>
      <button type="button" onClick={() => Camera.turnOnFlashlight()}>Turn flashlight on</button>
      <button type="button" onClick={() => Camera.turnOffFlashlight()}>Turn flashlight off</button>
      <button type="button" onClick={captureImage}>Capture image</button>
      {image && <img src={image} alt="Captured" />}
    </div>
  );
}
```

## turnOnFlashlight() and turnOffFlashlight()

Turns the scanner flashlight on or off.

```jsx
function FlashlightButton() {
  return <button type="button" onClick={() => Camera.turnOnFlashlight()}>On</button>;
}
```

Both methods return `Promise<void>`.

## openScanner() and closeScanner()

Starts or stops the native scanner overlay.

```jsx
function ScannerButton() {
  const open = async () => Camera.openScanner();
  const close = async () => Camera.closeScanner();
  return (
    <>
      <button type="button" onClick={open}>Start scanner</button>
      <button type="button" onClick={close}>Stop scanner</button>
    </>
  );
}
```

Both methods return `Promise<void>`.

## resumePreview() and pausePreview()

Resumes or pauses the active scanner preview. The scanner must be open first.

```jsx
function PreviewControls() {
  return (
    <>
      <button type="button" onClick={() => Camera.pausePreview()}>Pause</button>
      <button type="button" onClick={() => Camera.resumePreview()}>Resume</button>
    </>
  );
}
```

Both methods return `Promise<void>`.

## captureImage(width?)

Captures an image from the active camera.

```jsx
const capture = async () => {
  const result = await Camera.captureImage(300);
  // result.imageData is base64 encoded JPEG data
};
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `width` | `number` | no | Desired image width. The image ratio is preserved. |

Returns a `Promise` containing:

```js
{ imageData: string, format: 'jpeg' }
```
