---
stoplight-id: ms4oo1tuprpdj
---

# View

The View component wraps the content of every route in the application with a scrolling container and some
styling rules.

## Usage

```jsx
import { useTheme } from '@shopgate/engage/core';

function MyPageComponent() {
  const { View } = useTheme();

  return (
    <View>
      {/* your page content goes here */}
    </View>
  );
}
```

## Props

| Name               | Type      | Default                    | Description                                                      |
| ------------------ | --------- | -------------------------- | ---------------------------------------------------------------- |
| __children *__     | _node_    |                            | The content of the component.                                    |
| background         | _string_  | `themeConfig.colors.light` | The background color of the view.                                      |