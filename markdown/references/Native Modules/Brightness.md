---
stoplight-id: 1qs7qsxhn75m5
---

# Brightness

The Brightness module reads and changes the device screen brightness. It is available from the native modules package and is intended to be called from React event handlers or effects.

```jsx
import { Brightness } from '@shopgate/native-modules';
```

Brightness values are percentages from `0` (minimum) to `100` (maximum). Brightness changes require a real device; simulator behavior may vary by platform.

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { Brightness } from '@shopgate/native-modules';

export function BrightnessControls() {
  const [currentBrightness, setCurrentBrightness] = useState(null);

  useEffect(() => {
    const loadBrightness = async () => {
      const value = await Brightness.getBrightness();
      setCurrentBrightness(value);
    };

    loadBrightness();
  }, []);

  const setBrightness = async (brightness) => {
    await Brightness.setBrightness({ brightness });
    setCurrentBrightness(brightness);
  };

  return (
    <div>
      <p>Current brightness: {currentBrightness ?? 'unknown'}%</p>
      <button type="button" onClick={() => setBrightness(20)}>20%</button>
      <button type="button" onClick={() => setBrightness(50)}>50%</button>
      <button type="button" onClick={() => setBrightness(100)}>100%</button>
      <button
        type="button"
        onClick={async () => {
          await Brightness.resetBrightness();
          setCurrentBrightness(null);
        }}
      >
        Reset
      </button>
    </div>
  );
}
```

## setBrightness(params)

Sets the screen brightness.

```javascript
await Brightness.setBrightness({ brightness: 50 });
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `brightness` | `number` | yes | Brightness percentage from `0` to `100`. |

Returns a `Promise<void>`.

## getBrightness()

Returns the current screen brightness percentage.

```javascript
const brightness = await Brightness.getBrightness();
```

Returns a `Promise<number>`.

## resetBrightness()

Restores the device's default brightness.

```javascript
await Brightness.resetBrightness();
```

Returns a `Promise<void>`.

