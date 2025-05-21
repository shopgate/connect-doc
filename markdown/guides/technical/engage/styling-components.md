## Glamor (recommended)

Glamor is a library you can use to style components using JavaScript. You can read the [official documentation](https://github.com/threepointone/glamor/blob/master/README.md) to learn more about the API.

We recommend using Glamor because the CSS styles are encapsulated under content-based hashes. The benefit is that no component can accidentally overwrite the styling of another when using simple class selectors.

The following style declaration generates a hash of `css-59wjlk` which is the class that is appended to the DOM element.

### The style definition

```jsx
import { css } from 'glamor';

export default css({
  display: 'flex',
  padding: 10,
});
```

### Usage in the component

```jsx
import React from 'react';
import styles from './style';

function SimpleComponent({ children }) {
  return (
    <div className={styles}>
      {children}
    </div>
  );
}

export default SimpleComponent;
```

## CSS

You can create CSS files and import them when necessary, using the following code:

```css
.example-class {
  display: flex;
  padding: 10px;
}
```

Then you apply a simple CSS class in the React component:

```jsx
import React from 'react';
import './style.css';

function SimpleComponent({ children }) {
  return (
    <div className="example-class">
      {children}
    </div>
  );
}

export default SimpleComponent;
```

## Inline styles

React also supports inline styles. While this is the easiest method of adding styles to components, we only recommended using this method when there are styles that are determined by the React component state.

```js
import React from 'react';

class SimpleComponent extends React.Component {
  state = {
    error: true
  }

  render() {
    const { children } = this.props;
    const { error } = this.state;

    // The state determines the color of the text.
    const color = error ? 'red' : 'inherit';

    return(
      <div style={{ color }}>
        {children}
      </div>
    );
  }
}

export default SimpleComponent;
```
