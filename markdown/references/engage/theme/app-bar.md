---
stoplight-id: z9un73aryp868
---

# AppBar

The App Bar is used for branding, screen titles, navigation and actions. In iOS this bar is usually called Navigation Bar.

## Basic Usage

```jsx
import { useTheme } from '@shopgate/engage/core';

function MyPageComponent() {
  const { View, AppBar } = useTheme();

  return (
    <View>
      <AppBar title="My page title"/>
      {/* your page content goes here */}
    </View>
  );
}
```

## Custom Left Action

```jsx
import { useTheme } from '@shopgate/engage/core';
import { CrossIcon, AppBarAndroid } from '@shopgate/engage/components';

function CustomLeftAction() {
  function handleClick() {
    // Perform some action here.
  }

  return <AppBarAndroid.Icon icon={CrossIcon} onClick={handleClick} />;
}

function MyPageComponent() {
  const { View, AppBar } = useTheme();

  return (
    <View>
      <AppBar title="My page title" left={CustomLeftAction} />
      {/* your page content goes here */}
    </View>
  );
}

```

## Props

| Name            | Type        | Default                                | Description                                                                                   |
| --------------- | ----------- | -------------------------------------- | --------------------------------------------------------------------------------------------- |
| title           | _string_    | `null`                                 | The page title to display.                                                                    |
| left            | _Component_ | `<ArrowIcon />`                        | The component for rendering the left actions.                                                 |
| center          | _Component_ | `<AppBar.Title />`                     | The component for rendering the center display. By default this will render the `title` prop. |
| right           | _Component_ | `<SearchButton />` && `<CartButton />` | The component to render the right actions.                                                    |
| below           | _Component_ | `<ProgressBar />`                      | The component to render below the main contents of the App Bar.                               |
| backgroundColor | _string_    | `#fff`                                 | The background color.                                                                         |
| textColor       | _string_    | `#000`                                 | The text color.                                                                               |
| shadow          | _boolean_   | `true`                                 | Whether the App Bar should have a shadow.                                                     |