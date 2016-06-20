# Flexitive Page API Guide

## Overview
The Page API is a way to customize pages built in [Flexitive](https://flexitive.com). The Page API enables creation of custom elements, integrating with 3rd party tracking, and consuming external data feeds.

**This guide is a work-in-progress, expect breaking changes in the coming weeks and months**

## Getting Started
Pages exported from Flexitive automatically includes the Page API. In `index.html` you will find an empty `<script>` block in which to place your code.

## Custom elements
*Custom elements* are a special kind of element added to page in the Flexitive editor. These elements are defined at runtime using the Page API. This includes:

* how the element looks
* how the element changes over time
* how the element responds to user-initiated events

When exporting a page, Flexitive will automatically include skeleton API code for any custom elements, e.g.:

```javascript
Flexitive.customElement('ImpressiveAnimation', {
  load (callback) {
    // load element assets, callback when done
  }
  initialize (element, size) {
    // populate element with custom code
  }
  resize (element, size) {
    // called whenever the element changes size
  }
  appear () {
    // called when element appears in animation
  }
  disappear () {
    // called when element disappears in animation
  }
  stop () {
    // called when element should stop/skip its animation
  }
});
```

Custom elements always have a unique name which allows them to be referenced in code.

Defining a custom element involves defining several API hooks which are called by the Flexitive Runtime when the page loads. These API hooks are described below.

### `load`
Load any data (images/videos/json etc) required by the element and call `callback` when ready.

`load` is called by the Flexitive Runtime early in the page load sequence. The page will not start until all elements have finished loading their assets.

### `initialize`
Populate `element` with HTML you want to display when the element appears.

`size` is an object with `width` and `height` properties, representing the dimensions of the custom element. This is useful if the element content needs to respond to the element size.

### `resize` (optional)
Update the element HTML content whenever the window sizes changes.

### `appear` (optional)
Do something when the element appears.

### `disappear` (optional)
Do something when the element disappears.

### `stop` (optional)
Do something when the page has been "stopped" - an example would be if the user initiates a clickthrough. An example response would be to stop any video/audio playing in the element.
