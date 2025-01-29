## Introduction

Engage provides a form composition feature to build forms using a config. This feature can render form elements of any supported or custom type and handles element rendering and updates. It also propagates changes to the parent component and can take validation
errors from the parent to mark fields. The Form Builder allows fully customizable styling of
predefined elements and even defines custom element types.

The Form Builder also supports an advanced action system, which is not covered in this guide.

## Getting started

To add a form using the Form Builder with basic types:

- Import the Form Builder.
- Define a form config.
- Render the FormBuilder component, using the form config and a custom change handler.

### Setting up the config

The Form Builder renders all form elements based on a config.
Below is an example config containing one single form element.

```jsx
// File: CustomForm.config.js

const formConfig = {
  fields: {
    firstName: {
      type: 'text',
      sortOrder: 1,
      label: 'First name',
      placeholder: 'Enter your first name here',
    },
  },
};

export default formConfig;
```

### Using the Form Builder
Here, we import the previously created example config and render the form using the Form Builder.
For now, there is no validation.

```jsx
// File: CustomForm.jsx

import React, { useState } from 'react';
import { FormBuilder } from '@shopgate/engage/components';
import config from './CustomForm.config';

/**
 * A component that displays a form using the Form Builder
 * @returns {JSX}
 * @constructor
 */
const CustomForm = () => {
  // Save all data in the state of the current component to show a visual representation of it below
  const [formData, setFormData] = useState({});
  const [hasErrors, setHasErrors] = useState(false);

  return (
    <>
      <FormBuilder
        name="MyForm"
        config={config}
        handleUpdate={(data, hasErrs) => {
          setFormData(data);
          setHasErrors(hasErrs);
        }}
      />

      {/* Visualisation of the form data and the hasErrors flag */}
      <pre
        style={{
          backgroundColor: '#f4f4f4',
          border: '1px solid black',
          padding: '10px',
          whiteSpace: 'pre-wrap',
        }}
      >
        {JSON.stringify({ formData })}

        {JSON.stringify({ hasErrors })}
      </pre>
    </>
  );
};

export default CustomForm;
```

In its simplest form, it is just a matter of rendering the `FormBuilder` component and passing a config
to it.
Whenever the form data changes, the `handleUpdate` function is called with the form data
as the first argument. The second argument is true when any required field is either not
filled out or marked as invalid by form actions. Form actions could also cause fields to become
empty and thus render them invalid.

## FormBuilder component props

- Property: `name`<br />
  Type: String<br />
  Required: Yes<br />
  Comment: The name is added as the class attribute of the form tag in DOM, identifies
  the form, and groups form elements. The name should be unique among sibling forms when multiple
  forms are rendered next to each other.<br />

- Property: `config`<br />
  Type: Object<br />
  Required: Yes<br />
  Comment: The config defines what the Form Builder should render and how to behave.<br />

- Property: `handleUpdate`<br />
  Type: Function<br />
  Required: Yes<br />
  Function arguments:
  - `formData`: An object containing key/value pairs with the data per form element.
  - `hasErrors`: A boolean flag that defines whether the form data is valid in the current state or
  not.<br />

  Comment: This property propagates all form data changes to the higher component in the tree.
  It allows the parent component to react on user input. When reading inputs, it is necessary
  to distinguish between predefined field identifiers and custom ones. When a custom field notifies
  about a change, its value is located within a top level property called `customAttributes`, which
  itself is stored in the formData argument.<br />
  The change handler is run immediately on first render to report the current data after applying
  default values to all fields.

- Property: `className`<br />
  Type: Object or string<br />
  Required: No<br />
  Comment: The class name is inserted into the wrapper that contains all form elements. This allows
  inserting custom styling into the rendered form to override default form element styles. Each form
  element can be referenced with a static class name, e.g. `textField`. Custom styling is covered
  later in this guide.<br />

- Property: `defaults`<br />
  Type: Object<br />
  Required: No<br />
  Comment: Provides overriding default values for the form as key/value pairs. This is useful for
  context sensitive default values (e.g. based on locales).

- Property: `elements`<br />
  Type: Object<br />
  Required: No<br />
  Comment: Allows the replacement of default form elements or even introducing custom
  form element types which do not yet exist. For example, an image or
  swatch selector, or even elements that need no visuals, like hidden elements.

- Property: `onSubmit`<br />
  Type: Function<br />
  Required: No<br />
  Comment: This function is called whenever the form is submitted. The only argument is the submit
  event itself, per HTML standard.

- Property: `validationErrors`<br />
  Type: Array of validationError objects<br />
  Required: No<br />
  ValidationError object properties:
  * `path`: A string to identify the form element where the validation error occurs.
  * `message`: The message to display near the form element.

  Comment: Most form elements define a place that shows validation errors, when the input is
  incorrect or any other issue applies to the given form element. The Form Builder routes validation
  errors only to those form elements that are affected. The form elements can then decide
  whether to show any messages or not - for default elements, usually red text below the input
  field displays.

## Form config in detail

### Field identifiers

The Form Builder was initially designed to support a few predefined form fields.<br />
These fields are identified using the following keys:
- `firstName`
- `lastName`
- `street1`
- `street2`
- `zipCode`
- `city`
- `country`
- `province`

A form config that defines a `firstName` field is listed as an example above.
The type of these fields is not predefined and can be chosen based on the application's needs.

In addition to predefined fields, you can also define custom fields of any type.<br />
To achieve this, there is a special field name called `custom`. Here is an example config that
defines two custom fields, with the field identifiers `nickname` and `favoriteColor`:

```jsx
// File: CustomForm.config.js

const formConfig = {
  fields: {
    custom: {
      nickname: {
        type: 'text',
        sortOrder: 1,
        label: 'Nickname',
        placeholder: 'Enter your nickname here',
      },
      favoriteColor: {
        type: 'select',
        sortOrder: 2,
        label: 'Favorite color',
        default: '',
        options: {
          '': '',
          '01-red': 'Red',
          '02-blue': 'Blue',
        },
      },
    },
  },
};

export default formConfig;
```

### Element types

Out of the box, the Form Builder visually supports four groups of element types:
- Input field
  - `text` is a normal text input field without any specialties. The input return is of type
  `string`.
  - `email` supports email validation of the mobile browser. The input return type is `string`.
  - `password` obscures the input. The input return type is `string`.
  - `date` allows the selection of a date. The input return type is `string`.
  - `number` allows input of numbers only and opens a numpad keyboard only. The input return
  type is `string`.
  - `phone` refers to the "tel" html input element. The input return type is `string`.

- Checkbox
  - `checkbox` is a normal checkbox element that returns a `boolean` value.

- Radio group
  - `radio` renders a radio group with radio elements that are defined as key/value pairs in the
  `options` property of the field definition. The selected option is returned as a `string`.

- Select box
  - `select` renders a normal single line select box. As with the `radio` type, this element also
  takes an `options` property to fill the select box. The return of the selection is also a
  string. The previous example shows how such a select box looks.
  - `country` is a special type of select box with the difference that it takes a `countries`
  property instead of `options`. The countries must be defined as an object with key/value pairs
  where the key is the country code (in the ISO-3166-2 format) and the name as the value.
  - `province` is a special kind of select box as well. It relies on an element of type `country`
  to exist in the form and is context sensitive to it. Based on the selected country, the
  `province` element changes its values to only show provinces that exist in that country.

Besides the types listed above, it is also possible to define form elements which are not supported
out of the box. See section "Advanced customization".

### Field properties in detail

Every field definition generally looks like this:
```json
{
  "firstName": {
    "type": "text",
    "label": "First name"
  }
}
```

This is the minimal requirement for a field definition. For radio and the basic select types, you must provide an `options` property, otherwise there will not be any options to select.

#### Here is a complete list of supported properties:

- `type` has been explained in the section "Field types" already.

- `sortOrder` is useful to enable placement of custom fields between fields outside the `custom`
property, within the field config.
This can be a positive integer or float value. If no `sortOrder` is set, the element is
placed below predefined field IDs and also below fields that define a sort order. The elements are
always sorted in ascending order.

- `label` defines the text to be shown to the user.

- `placeholder` Is the text to be shown for elements of type `text` when the field does not contain
any input.

- `default` defines a value that pre-fills the element with a value before the form is presented to
the user. For checkboxes `default` is a `boolean` value and `string` for all other types.
Please note that the empty string is considered as a valid default value. If a field is not
supposed to have a default value, then this property must be removed or be set to `null`.

- `options` only applies to elements of type `radio` and `select`. It is represented with an object
that contains a key/value pair for every item or option entry. The key is the selection ID and the
value is the display text. Whenever a selection is made, the handler of the Form Builder is called
and the selected value is the selection identifier.

- `countries` is only used for elements of type `country`. The selection is referred to by the
countryCode which is the key of the respective entry. More details about this are provided in the
previous section about "Field types".

- `actions` allow context sensitive behavior of the Form Builder. An action can be an input
restriction, input transformation, showing or hiding related form elements, and more.
Since it is a more advanced feature, it is not covered in detail here.

- `required` defines if the field is allowed to be submitted empty or not. This must be a boolean
value. A field can only be required when it is visible.

- `visible` indicates whether to show or hide an element in the form. Logically, elements
that are not visible cannot be marked as `required`.

## Overriding defaults

When using the Form Builder, it is possible to pass default values for each form element. This is
useful in situations where the default value is context sensitive or when the form is pre-filled
with values from an API.

If the `defaults` prop is used it will have a higher priority than what is set in the form config.
Other than that, it is still treated as a conventional default value and can be changed via
interaction with the from.

To assign a default value to a form element on initial rendering, it is once more necessary to
distinguish between defaults for predefined form identifiers and custom form identifiers.

### Providing a default value for a predefined form element

```jsx
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    config={config}
    handleUpdate={() => { /* Don't handle updates in this example */ }}

    defaults={{
      firstName: 'John',
    }}
  />
);

export default CustomForm;
```

### Providing a default value for a custom form element

```jsx
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    config={config}
    handleUpdate={() => { /* Don't handle updates in this example */ }}

    defaults={{
      customAttributes: {
        nickname: 'Jonny',
        favoriteColor: '02-blue', // "02-blue" is key of the option to select, not the display text
      },
    }}
  />
);

export default CustomForm;
``` 

The above example shows two different kinds of defaults. One is an element of type `text`, while the
second is of type `select`. The defaults for `select` and `radio` are applied using the options key
or the countryCode for type `country`.
The only difference is the additional property with the name `customAttributes` where all custom
field defaults are placed.

## Displaying validation errors

By using the `validationErrors` property, it is possible to provide an array of validation errors to
targeted elements in the form. All form elements natively supported by the Form Builder provide a
way to show validation errors.

A single validation error object is represented with a path and a message like this:

```json
{
  "path": "field-identifier",
  "message": "Custom error text to display below the field."
}
```

The path references the field identifier and the message is just plain text.

To display validation errors, simply pass one or more ValidationError objects within an array to the
Form Builder using the `validationErrors` prop like this:

```jsx
const CustomForm = () => {
  const demoValidationErrors = [{
    path: 'nickname',
    message: 'The nickname must be at least 3 characters long',
  }];

  return (
    <FormBuilder
      name="MyForm"
      config={config}
      handleUpdate={() => { /* Don't handle updates in this example */ }}

      validationErrors={demoValidationErrors}
    />
  );
};

export default CustomForm;
```

Please be aware that a change in the form input will clear out the validation error automatically.
This is useful in cases when the validation errors are checked after submission (usually done by
APIs).<br />
Mutating validation errors in the `handleUpdate` prop is not supported, because of the automatic
handling. Trying to do that anyway will most likely result in unexpected behavior.

Validating input and applying a message on every change can be done by adding a validation layer
between the Form Builder and the elements it renders. An example of how to achieve this is shown
in the section about advanced customization.

## Applying custom styles

Every form element comes with a fixed class name, which allows styling. The Form Builder
takes a `className` property for that purpose and allows element styling with glamor.

The following example changes the validation error message of the text input for the first name to
appear in blue instead of the default red color. It also changes the error text of the
last name field to become bold and be shown in a bigger font size:

```jsx
// File: CustomForm.jsx

import React, { useState } from 'react';
import { css } from 'glamor';
import { FormBuilder } from '@shopgate/engage/components';

const config = {
  fields: {
    firstName: {
      type: 'text',
      sortOrder: 1,
      label: 'First name',
      placeholder: 'Enter your first name here',
    },
    lastName: {
      type: 'text',
      sortOrder: 1,
      label: 'Last name',
      placeholder: 'Enter your last name here',
    },
  },
};

/**
 * A component that displays a form using the Form Builder
 * @returns {JSX}
 * @constructor
 */
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    config={config}
    handleUpdate={() => { /* Don't handle updates in this example */ }}

    validationErrors={
      // Add validation errors to both fields to visualize the styling changes
      [{
        path: 'firstName',
        message: 'Invalid first name',
      }, {
        path: 'lastName',
        message: 'Invalid last name',
      }]
    }

    className={css({
      // Define custom selectors for the form inputs and style them
      ' .myFormFirstName .errorText': {
        color: 'blue',
      },
      ' .myFormLastName .errorText': {
        fontWeight: 'bold',
        fontSize: '1rem',
      },
    }).toString()}
  />
);

export default CustomForm;
```

The easiest way to find the class names to create CSS selectors is to render the fields first and
then inspect the DOM to get the desired class name to target the element that should be styled.

Generally the following rules apply:
- Every element is wrapped in a container that gets a unique element class name. It is a combination
of the form name (passed to the Form Builder) and the field ID. Those are then transformed to
camelCase.<br />In the upper example, the form name is `MyForm` and the field to be rendered is
`firstName`, which results in the class name `myFormFirstName` which is then referred to via the CSS
selector.
- Text field wrappers expose the class name `textField`.
- Hint blocks within elements include the class name `hint`.
- Labels come with a class name called `label`.
- Placeholders use the class name `placeholder`. 
- The underline shown below text elements includes the class name `underline`.
- Error text fields in form elements get the class name `errorText`.
- Radio group wrappers in the DOM include the class name `radioGroup`.
- Radio item labels wrap the whole radio item and two additional class names apply. The first
class name is the radio item key name and the second one is `radioItem`.
- Input fields can be either text inputs with the class name `simpleInput` or `multilineInput` or
they can be input types like radio input fields that expose the class name `input`.
- Select fields come with the class name `select`.
- Select option items are marked with the class name `option`.

## Advanced customization

The Form Builder not only renders the included elements, it also allows adding custom
element types or even replacing existing ones.

### Defining a custom element

A form element is basically a React component that receives a few props like the field data and the
current value. Whenever the value of the field changes it should report the new value to the Form
Builder so it can apply form actions and pass the value up to the parent component.

A custom element can be defined like this:

```jsx
// File: ElementHiddenValue.jsx

import React from 'react';
import PropTypes from 'prop-types';

/**
 * Renders a hidden field into the DOM and some info in "pre" tags below that.
 * @param {Object} element The field data from the config along with some additional attributes.
 * @param {string} value This is the indicator if the element should render or not
 * @returns {JSX}
 */
const ElementHiddenValue = ({ element, ...restProps }) => (
  <>
    <input
      type="hidden"
      value={restProps.value}
    />

    {/* Visualisation of the element props from the FormBuilder */}
    <pre>{JSON.stringify(element)}</pre>
    <pre>{JSON.stringify(restProps)}</pre>
  </>
);

ElementHiddenValue.propTypes = {
  element: PropTypes.shape().isRequired,
  value: PropTypes.bool.isRequired,
};

ElementHiddenValue.defaultProps = {};

export default ElementHiddenValue;
```

Every element receives the following props from the Form Builder:

- `element`: This is an object containing the configuration for the specific field. These are all
properties that are documented above, but not limited to that. Every additional property in the
field config is passed to the custom element as shown in the next demo. Additionally, it
gets an `id` and a `handleChange` property. It also gets a boolean property called `custom` to distinguish between predefined and custom field identifiers.<br />
Reserved attribute names:
  - id
  - handleChange
  - custom
  - value

- `errorText`: This prop stores the text to display when a validation error is
shown for the field.

- `name`: The name prop is a concatenation of the form name and the field ID. It is useful as a
class name or as prefix of a key, if the custom component renders multiple components in a loop.

- `value`: The value to be shown in the element. This can be anything specific to the element.
It is good practice to always use the `value` prop instead of maintaining an internal state,
because the Form Builder needs to be able to change it.
Whenever the value changes or is supposed to change  the `handleChange` function is called
like this: `element.handleChange(newValue);` (when the `element` prop is taken in the component as
in the example above).

- `visible`: By default, elements are visible and can be hidden while still present in the form.
When the custom element is supposed to be toggleable, this prop is a good candidate because
it is fully supported by the Form Builder.<br />
Please note that the `element` prop might also contain a `visible` attribute, but it always
contains the initial value from the field config and is not updated to the current visibility
state. In other words, always use the `visible` prop and never `element.visible` to get the
visibility state of a field.

### Integrating a custom element type

The following code example defines a new form element that shows a box with some info text, with the
ability to collapse:

```jsx
// File: ElementInfobox.jsx

import React from 'react';
import PropTypes from 'prop-types';
import { css } from 'glamor';
import classNames from 'classnames';

const style = {
  infoboxContainer: css({
    padding: '.5rem',
    margin: '1rem .25rem',
    border: '2px solid #b3b300',
    backgroundColor: '#ffffe6',
    borderRadius: '.4rem',
  }).toString(),
  infoboxContent: css({
    paddingLeft: '.5rem',
    borderLeft: '.5rem solid #b3b300',
    borderRadius: '.4rem',
  }).toString(),
  header: css({
    padding: '.5rem 0',
    display: 'flex',
    justifyContent: 'space-between',
    alignItems: 'center',
  }).toString(),
  titleText: css({
    fontWeight: 'bold',
    fontSize: '1.3rem',
  }).toString(),
  titleButton: css({
    border: '1px dashed #b3b300',
    borderRadius: '.4rem',
    width: '100px',
    outline: 'none',
  }).toString(),
  separator: css({
    marginTop: 0,
  }).toString(),
};

/**
 * Renders a custom form element with type "infobox". It does not allow input, but can be closed by
 * clicking on it. When the box closes, it informs the FormBuilder that its value has changed to false.
 * @param {Object} element The field data from the config along with some additional attributes.
 * @param {boolean} value Indicates if the element should render or not.
 * @param {boolean} visible Indicates if the element is shown.
 * @returns {JSX}
 */
const ElementInfobox = ({
  element, name, value, visible,
}) => {
  // Don't render anything, when it's invisible.
  if (!visible) {
    return null;
  }

  return (
    <div
      role="note"
      className={classNames(style.infoboxContainer, name)}
    >
      <div className={classNames(style.infoboxContent, name)}>
        <div
          role="heading"
          className={style.header}
        >
          <div className={style.titleText}>{element.title}</div>
          <button
            type="button"
            className={style.titleButton}
            onClick={() => element.handleChange(!value)}
          >
            {value && <span>collapse</span>}
            {!value && <span>expand</span>}
          </button>
        </div>

        {value && <hr className={style.separator} />}
        {value &&
        element.text
          .replace(['<br>', '<br />'], '<br/>')
          .split('<br/>')
          .map((textEntry, i) => <div key={`${i + 1}`}>{textEntry}</div>)
        }
      </div>
    </div>
  );
};

ElementInfobox.propTypes = {
  element: PropTypes.shape().isRequired,
  name: PropTypes.string.isRequired,
  value: PropTypes.bool.isRequired,
  visible: PropTypes.bool,
};

ElementInfobox.defaultProps = {
  visible: true,
};

export default ElementInfobox;
```

Now it's time to define a config and register it to the Form Builder to be rendered:

```jsx
// File: CustomForm.jsx

import React from 'react';
import { FormBuilder } from '@shopgate/engage/components';
import ElementInfobox from './ElementInfobox';

const ELEMENT_TYPE_INFOBOX = 'infobox';
const config = {
  fields: {
    custom: {
      info: {
        type: ELEMENT_TYPE_INFOBOX,
        label: '', // The custom element does not use the label
        title: 'Demo title',
        default: true, // Initialize the element with true to start up in expanded state
        text: // This is a completely custom attribute
          'This is a custom text with in the body of the infobox element.<br/>Click me to close!',
      },
    },
  },
};

/**
 * A component that displays a form using the Form Builder
 * @returns {JSX}
 * @constructor
 */
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    handleUpdate={() => { /* Don't handle updates in this example */ }}
    config={config}
    elements={{
      [ELEMENT_TYPE_INFOBOX]: ElementInfobox,
    }}
  />
);

export default CustomForm;
```

### Replacing existing element types

Any existing element type can be either replaced with a completely custom element or can be wrapped
with additional logic. Thus, additional logic can be achieved, like dynamic validation errors.

To replace an element, just put it into the `elements` prop of the FormBuilder component, as shown in
the example above. The
`elements` prop is simply a key/value pair with the key being the `type` string and value being a
React node.

All available element type names are exposed via constants in the Engage library at this location:
`@shopgate/engage/components/Form/Builder/Builder.constants`.

Existing form elements can also be imported to use within a custom element. Simply import the
one to be wrapped and render it within a custom component:
- `@shopgate/engage/components/Form/Builder/ElementText`
- `@shopgate/engage/components/Form/Builder/ElementCheckbox`
- `@shopgate/engage/components/Form/Builder/ElementRadio`
- `@shopgate/engage/components/Form/Builder/ElementSelect`

The following example demonstrates how to replace all elements of type `select` with elements of
type `radio`. This is possible because these two specific elements work in a similar fashion and
expose the same interface for their usage:

```jsx
// File: CustomForm.jsx

import React from 'react';
import { FormBuilder } from '@shopgate/engage/components';
import { ELEMENT_TYPE_SELECT } from '@shopgate/engage/components/Form/Builder/Builder.constants';
import ElementRadio from '@shopgate/engage/components/Form/Builder/ElementRadio';

const config = {
  fields: {
    custom: {
      favoriteColor: {
        type: 'select',
        sortOrder: 2,
        label: 'Favorite color',
        options: {
          '01-red': 'Red',
          '02-blue': 'Blue',
        },
      },
    },
  },
};

/**
 * A component that displays a form using the Form Builder
 * @returns {JSX}
 * @constructor
 */
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    config={config}
    handleUpdate={() => { /* Don't handle updates in this example */ }}
    elements={{
      [ELEMENT_TYPE_SELECT]: ElementRadio, // Every select box is now rendered as a radio group
    }}
  />
);

export default CustomForm;
```

### Achieving form validation using custom elements

In the last section, there was a hint that a custom element can be created or existing elements be
reused by importing and rendering them.
This allows extending elements without changing their basics and how they operate.

The following code example wraps the original text element to add advanced validation for the
nickname field. Meanwhile, it keeps the look and feel of the original text field.<br />
It just adds an error text when the nickname is shorter than 3 characters or longer than 20.

```jsx
// File: ElementCustomText.jsx

import React from 'react';
import PropTypes from 'prop-types';
import ElementText from '@shopgate/engage/components/Form/Builder/ElementText';

/**
 * Validates the data and returns an error string if invalid
 * @param {string} id The field identifier
 * @param {string} value The value to be validated
 * @returns {string}
 */
const validate = (id, value) => {
  // Validate the nickname field only
  if (id !== 'nickname') {
    return '';
  }

  if (value.length < 3) {
    return 'The nickname can not be shorter than 3 letters';
  }

  if (value.length > 20) {
    return 'The nickname is too long';
  }

  return '';
};

/**
 * Passes though all props except errorText, which is hydrated with validation
 * @param {string} errorText Incoming error text
 * @param {Object} restProps All other props that are set by the Form Builder
 * @returns {JSX}
 */
const ElementCustomText = ({ errorText, ...restProps }) => {
  const { element, value } = restProps;
  return <ElementText {...restProps} errorText={validate(element.id, value)} />;
};

ElementCustomText.propTypes = {
  errorText: PropTypes.string.isRequired,
};

export default ElementCustomText;
```

Now this component can be used to replace the existing text element.

```jsx
// File: CustomForm.jsx

import React from 'react';
import { FormBuilder } from '@shopgate/engage/components';
import { ELEMENT_TYPE_TEXT } from '@shopgate/engage/components/Form/Builder/Builder.constants';
import ElementCustomText from './ElementCustomText';

const config = {
  fields: {
    custom: {
      nickname: {
        type: 'text',
        label: 'Nickname',
      },
    },
  },
};

/**
 * A component that displays a form using the Form Builder
 * @returns {JSX}
 * @constructor
 */
const CustomForm = () => (
  <FormBuilder
    name="MyForm"
    handleUpdate={() => { /* Don't handle updates in this example */ }}
    config={config}
    elements={{
      [ELEMENT_TYPE_TEXT]: ElementCustomText, // Replaces the text element with a custom one
    }}
  />
);

export default CustomForm;
```

### Integration with form actions

Form actions should be automatically supported with any custom element, as long as the provided
`element.handleChange` function is called for value updates instead of locally storing and changing
the value manually. That of course also means that form actions rely on the value and/or visibility
prop actually being used by the custom element. If the custom element does not use either one, then
form actions do not apply or have no effect on the custom element.
