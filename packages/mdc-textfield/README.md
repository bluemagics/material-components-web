<!--docs:
title: "Text Fields"
layout: detail
section: components
iconId: text_field
path: /catalog/input-controls/text-fields/
-->

# Text Fields

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/textfield.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/textfields.png" width="240" alt="Text fields screenshot">
  </a>
</div>-->

The MDC Text Field component provides a textual input field adhering to the [Material Design Specification](https://material.io/guidelines/components/text-fields.html).
It is fully accessible, ships with RTL support, and includes a gracefully-degraded version that does
not require any javascript.

## Design & API Documentation

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/text-fields.html">Material Design guidelines: Text Fields</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/textfield.html">Demo</a>
  </li>
</ul>

## Installation

```
npm install --save @material/textfield
```

## Usage

### Single-line - with Javascript

```html
<div class="mdc-textfield">
  <input type="text" id="my-textfield" class="mdc-textfield__input">
  <label class="mdc-textfield__label" for="my-textfield">Hint text</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

It's also possible to wrap an input within a `<label>` to avoid dynamic id generation:

```html
<label class="mdc-textfield">
  <input type="text" class="mdc-textfield__input">
  <span class="mdc-textfield__label">Hint Text</span>
  <div class="mdc-textfield__bottom-line"></div>
</label>
```

> _NOTE_: Only place an `mdc-textfield__label` inside of a text field _if you plan on using
> Javascript_. Otherwise, the label must go outside of the textfield, as shown below.

### Single-line - Gracefully degraded

```html
<label for="textfield-no-js">Textfield with no JS: </label>
<div class="mdc-textfield">
  <input type="text" id="textfield-no-js" class="mdc-textfield__input" placeholder="Hint text">
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

### Disabled Text Fields

```html
<div class="mdc-textfield mdc-textfield--disabled">
  <input type="text" id="disabled-textfield" class="mdc-textfield__input" disabled>
  <label class="mdc-textfield__label" for="disabled-textfield">Disabled text field</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

### Pre-filled text fields

When dealing with JS-driven text fields that already have values, you'll want to ensure that you
render the text field label with the `mdc-textfield__label--float-above` modifier class. This will
ensure that the label moves out of the way of the text field's value and prevents a Flash Of
Un-styled Content (**FOUC**). You'll also want to add the `mdc-textfield--upgraded` modifier class
on the textfield root element. The JS component does for you automatically on initialization, but
since it won't be added until that JS runs, adding it manually will prevent an initial FOUC.

```html
<div class="mdc-textfield mdc-textfield--upgraded">
  <input type="text" id="pre-filled" class="mdc-textfield__input" value="Pre-filled value">
  <label class="mdc-textfield__label mdc-textfield__label--float-above" for="pre-filled">
    Label in correct place
  </label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

### Using help text

MDC Text Fields can include help text that is useful for providing supplemental
information to users, as well for validation messages (covered below).

```html
<div class="mdc-textfield">
  <input type="text" id="username" class="mdc-textfield__input" aria-controls="username-helptext">
  <label for="username" class="mdc-textfield__label">Username</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
<p id="username-helptext" class="mdc-textfield-helptext" aria-hidden="true">
  This will be displayed on your public profile
</p>
```

Help text appears on input field focus and disappears on input field blur by default when using
the textfield JS component.

#### Persistent help text

If you'd like the help text to always be visible, add the
`mdc-textfield-helptext--persistent` modifier class to the element.

```html
<div class="mdc-textfield">
  <input type="email" id="email" class="mdc-textfield__input">
  <label for="email" class="mdc-textfield__label">Email address</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
<p class="mdc-textfield-helptext mdc-textfield-helptext--persistent">
  We will <em>never</em> share your email address with third parties
</p>
```

#### Help text and accessibility

Note that in every example where the help text is dependent on the state of the input element, we
assign an id to the `mdc-textfield-helptext` element and set that id to the value of the
`aria-controls` attribute on the input element. We recommend doing this as well as it will help
indicate to assistive devices that the display of the help text is dependent on the interaction with
the input element.

When using our vanilla JS component, if it sees that the input element has an `aria-controls`
attribute, it will look for an element with the id specified and treat it as the text field's help
text element, taking care of adding/removing `aria-hidden` and other a11y attributes. This can also
be done programmatically, which is described below.

### Validation

MDC Textfield provides validity styling by using the `:invalid` and `:required` attributes provided
by HTML5's form validation API.

```html
<div class="mdc-textfield">
  <input type="password" id="pw" class="mdc-textfield__input" required minlength=8>
  <label for="pw" class="mdc-textfield__label">Password</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

By default an input's validity is checked via `checkValidity()` on blur, and the styles are updated
accordingly. Set the MDCTextfield.valid variable to set the input's validity explicitly. MDC Textfield
automatically appends an asterisk to the label text if the required attribute is set.

Help text can be used to provide additional validation messages. Use
`mdc-textfield-helptext--validation-msg` to provide styles for using the help text as a validation
message. This can be easily combined with `mdc-textfield-helptext--persistent` to provide a robust
UX for client-side form field validation.

```html
<div class="mdc-textfield">
  <input required minlength=8 type="password" class="mdc-textfield__input" id="pw"
         aria-controls="pw-validation-msg">
  <label for="pw" class="mdc-textfield__label">Choose password</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
<p class="mdc-textfield-helptext
          mdc-textfield-helptext--persistent
          mdc-textfield-helptext--validation-msg"
   id="pw-validation-msg">
  Must be at least 8 characters long
</p>
```

### Leading and Trailing Icons
Leading and trailing icons can be added to MDC Text Fields as visual indicators
as well as interaction targets. To do so, add the relevant classes
(`mdc-textfield--with-leading-icon` or `mdc-textfield--with-trailing-icon`) to the root element, add
an `i` element with your preferred icon, and give it a class of `mdc-textfield__icon`.

#### Leading:
```html
<div class="mdc-textfield mdc-textfield--box mdc-textfield--with-leading-icon">
  <i class="material-icons mdc-textfield__icon" tabindex="0">event</i>
  <input type="text" id="my-input" class="mdc-textfield__input">
  <label for="my-input" class="mdc-textfield__label">Your Name</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

#### Trailing:
```html
<div class="mdc-textfield mdc-textfield--box mdc-textfield--with-trailing-icon">
  <input type="text" id="my-input" class="mdc-textfield__input">
  <label for="my-input" class="mdc-textfield__label">Your Name</label>
  <i class="material-icons mdc-textfield__icon" tabindex="0">event</i>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

>**NOTE:** if you would like to display un-clickable icons, simply remove `tabindex="0"`,
and the css will ensure the cursor is set to default, and that actioning on an icon doesn't
do anything unexpected.


### Textarea

```html
<div class="mdc-textfield mdc-textfield--textarea">
  <textarea id="textarea" class="mdc-textfield__input" rows="8" cols="40"></textarea>
  <label for="textarea" class="mdc-textfield__label">Textarea Label</label>
</div>
```

### Textarea - CSS Only

```html
<div class="mdc-textfield mdc-textfield--textarea">
  <textarea id="textarea-css-only"
    class="mdc-textfield__input"
    rows="8"
    cols="40"
    placeholder="Enter something about yourself"></textarea>
</div>
```

### Full-width

```html
<div class="mdc-textfield mdc-textfield--fullwidth">
  <input class="mdc-textfield__input"
         type="text"
         placeholder="Full-Width Textfield"
         aria-label="Full-Width Textfield">
</div>

<div class="mdc-textfield mdc-textfield--fullwidth mdc-textfield--textarea">
  <textarea id="full-width-textarea" class="mdc-textfield__input" rows="8"></textarea>
  <label for="full-width-textarea" class="mdc-textfield__label">Textarea Label</label>
</div>
```

Note that **full-width text fields do not support floating labels**. Labels should not be
included as part of the DOM structure for full-width text fields. Full-width textareas
behave normally.

### Text Field Boxes

```html
<div class="mdc-textfield mdc-textfield--box">
  <input type="text" id="tf-box" class="mdc-textfield__input">
  <label for="tf-box" class="mdc-textfield__label">Your Name</label>
  <div class="mdc-textfield__bottom-line"></div>
</div>
```

Note that Text field boxes support all of the same features as normal textfields, including help
text, validation, and dense UI.

#### CSS-only text field boxes

```html
<label for="css-only-textfield-box">Your name:</label>
<div class="mdc-textfield mdc-textfield--box">
  <input type="text" class="mdc-textfield__input" id="css-only-textfield-box" placeholder="Name">
</div>
```

### Sass Mixins

To customize a Filled Text Field or a Text Field `textarea`'s border radius, you can use the following mixins.
Alternatively, if you would like to change the border radius for every instance of MDC Text Field uniformly, regardless
of the variant, you can override $mdc-text-field-border-radius in Sass.

#### `mdc-text-field-box-corner-radius($radius)`

This mixin customizes the border radius for a Text Field Box.

#### `mdc-text-field-textarea-corner-radius($radius)`

This mixin customizes the border radius for a Text Field `textarea`.

### Using the JS component

MDC Textfield ships with Component / Foundation classes which are used to provide a full-fidelity
Material Design text field component.

#### Including in code

##### ES2015

```javascript
import {MDCTextfield, MDCTextfieldFoundation} from '@material/textfield';
```

##### CommonJS

```javascript
const mdcTextfield = require('mdc-textfield');
const MDCTextfield = mdcTextfield.MDCTextfield;
const MDCTextfieldFoundation = mdcTextfield.MDCTextfieldFoundation;
```

##### AMD

```javascript
require(['path/to/mdc-textfield'], mdcTextfield => {
  const MDCTextfield = mdcTextfield.MDCTextfield;
  const MDCTextfieldFoundation = mdcTextfield.MDCTextfieldFoundation;
});
```

##### Global

```javascript
const MDCTextfield = mdc.textfield.MDCTextfield;
const MDCTextfieldFoundation = mdc.textfield.MDCTextfieldFoundation;
```

#### Automatic Instantiation

```javascript
mdc.textfield.MDCTextfield.attachTo(document.querySelector('.mdc-textfield'));
```

#### Manual Instantiation

```javascript
import {MDCTextfield} from '@material/textfield';

const textfield = new MDCTextfield(document.querySelector('.mdc-textfield'));
```

#### Controlling ripple instantiation

When `MDCTextfield` is instantiated with a root element containing the `mdc-textfield--box` class,
it instantiates an `MDCRipple` instance on the element in order to facilitate the correct
interaction UX for text field boxes as outlined in the spec. The way this ripple is instantiated
can be controlled by passing a ripple factory argument to the constructor.

```js
const textfieldBoxEl = document.querySelector('.mdc-textfield--box');
const textfield = new MDCTextfield(textfieldBoxEl, /* foundation */ undefined, (el) => {
  // do something with el...
  return new MDCRipple(el);
});
```

By default the ripple factory simply calls `new MDCRipple(el)` and returns the result.

#### MDCTextfield API

Similar to regular DOM elements, the `MDCTextfield` functionality is exposed through accessor
methods.

##### MDCTextfield.helptextElement

HTMLLabelElement. This is a normal property (non-accessor) that holds a reference to the element
being used as the text field's "help text". It defaults to `null`. If the text field's input element
contains an `aria-controls` attribute on instantiation of the component, it will look for an element
with the corresponding id within the document and automatically assign it to this property.

##### MDCTextfield.disabled

Boolean. Proxies to the foundation's `isDisabled/setDisabled` methods when retrieved/set
respectively.

##### MDCTextfield.valid

Boolean setter. Proxies to the foundation's `setValid` method when set.

##### MDCTextfield.ripple

`MDCRipple` instance. Set to the `MDCRipple` instance for the root element that `MDCTextfield`
initializes when given an `mdc-textfield--box` root element. Otherwise, the field is set to `null`.

### Using the foundation class

Because MDC Textfield is a feature-rich and relatively complex component, its adapter is a bit more
complicated.

| Method Signature | Description |
| --- | --- |
| addClass(className: string) => void | Adds a class to the root element |
| removeClass(className: string) => void | Removes a class from the root element |
| addClassToLabel(className: string) => void | Adds a class to the label element. We recommend you add a conditional check here, and in `removeClassFromLabel` for whether or not the label is present so that the JS component could be used with text fields that don't require a label, such as the full-width text field. |
| removeClassFromLabel(className: string) => void | Removes a class from the label element |
| eventTargetHasClass(target: HTMLElement, className: string) => boolean | Returns true if classname exists for a given target element |
| registerTextFieldInteractionHandler(evtType: string, handler: EventListener) => void | Registers an event handler on the root element for a given event |
| deregisterTextFieldInteractionHandler(evtType: string, handler: EventListener) => void | Deregisters an event handler on the root element for a given event |
| notifyIconAction() => void | Emits a custom event "MDCTextfield:icon" denoting a user has clicked the icon |
| addClassToBottomLine(className: string) => void | Adds a class to the bottom line element |
| removeClassFromBottomLine(className: string) => void | Removes a class from the bottom line element |
| addClassToHelptext(className: string) => void | Adds a class to the help text element. Note that in our code we check for whether or not we have a help text element and if we don't, we simply return. |
| removeClassFromHelptext(className: string) => void | Removes a class from the help text element. |
| helptextHasClass(className: string) => boolean | Returns whether or not the help text element contains the current class |
| registerInputInteractionHandler(evtType: string, handler: EventListener) => void | Registers an event listener on the native input element for a given event |
| deregisterInputInteractionHandler(evtType: string, handler: EventListener) => void | Deregisters an event listener on the native input element for a given event |
| registerTransitionEndHandler(handler: EventListener) => void | Registers an event listener on the bottom line element for a "transitionend" event |
| deregisterTransitionEndHandler(handler: EventListener) => void | Deregisters an event listener on the bottom line element for a "transitionend" event |
| setBottomLineAttr(attr: string, value: string) => void | Sets an attribute with a given value on the bottom line element |
| setHelptextAttr(name: string, value: string) => void | Sets an attribute with a given value on the help text element |
| removeHelptextAttr(name: string) => void | Removes an attribute from the help text element |
| getNativeInput() => {value: string, disabled: boolean, badInput: boolean, checkValidity: () => boolean}? | Returns an object representing the native text input element, with a similar API shape. The object returned should include the `value`, `disabled` and `badInput` properties, as well as the `checkValidity()` function. We _never_ alter the value within our code, however we _do_ update the disabled property, so if you choose to duck-type the return value for this method in your implementation it's important to keep this in mind. Also note that this method can return null, which the foundation will handle gracefully. |

#### The full foundation API

##### MDCTextfieldFoundation.isDisabled() => boolean

Returns a boolean specifying whether or not the input is disabled.

##### MDCTextfieldFoundation.setDisabled(disabled: boolean)

Updates the input's disabled state.

### Theming

MDC Textfield components use the configured theme's primary color for its underline and label text
when the input is focused.

MDC Textfield components support dark themes.
