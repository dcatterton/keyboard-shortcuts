# Expansion Panel

Expansion panels provide progressive disclosure of content. Use them to group and hide content that is not immediately relevant to the user. They are useful for organizing information and reducing clutter on the screen.

## Basic Example

```html
<forge-expansion-panel>
  <button 
    slot="header" 
    type="button" 
    aria-controls="content" 
    aria-expanded="false"
  >
    Toggle
  </button>
  <div id="content" role="group">
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis minus
      ut illum corporis incidunt quod temporibus consequatur rem! Libero rem
      nulla quod corporis similique consequuntur facere laborum veniam error
      eius.
    </p>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis minus
      ut illum corporis incidunt quod temporibus consequatur rem! Libero rem
      nulla quod corporis similique consequuntur facere laborum veniam error
      eius.
    </p>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis minus
      ut illum corporis incidunt quod temporibus consequatur rem! Libero rem
      nulla quod corporis similique consequuntur facere laborum veniam error
      eius.
    </p>
  </div>
</forge-expansion-panel>
```

## With Card

It's common to compose an expansion panel with a card component to provide a more visually appealing layout.

```html
<forge-card>
  <forge-expansion-panel>
    <div
      slot="header"
      role="button"
      tabindex="0"
      style="display: flex; justify-content: space-between;"
    >
      <div>Header text</div>
      <forge-open-icon></forge-open-icon>
    </div>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis minus
      ut illum corporis incidunt quod temporibus consequatur rem! Libero rem
      nulla quod corporis similique consequuntur facere laborum veniam error
      eius.
    </p>
  </forge-expansion-panel>
</forge-card>
```

> **Tip**: You can provide a `<forge-open-icon>` to show the open state of the expansion panel, and the icon will be rotated when the panel is opened/closed.

## Trigger Button

A button in the header slot of the expansion panel will automatically control toggling the open state of the panel. Setting the `trigger` attribute/property of the expansion panel to the button's id will also manage its `aria-expanded` and `aria-controls` attributes. You can also set `trigger` to the id of a button elsewhere in the document to add the toggling and ARIA attribute functionality to it.

> **Tip**: Make sure the intended trigger element is present in the DOM at the same time the expansion panel initializes or has trigger set. Alternatively, use the `triggerElement` property to directly pass in the trigger element reference, which is less prone to errors related to incremental rendering.

```html
<button id="button-id">Toggle</button>
<forge-card>
  <forge-expansion-panel trigger="button-id">
    <div
      slot="header"
      role="button"
      tabindex="0"
      style="display: flex; justify-content: space-between;"
    >
      <div>Header text</div>
      <forge-open-icon></forge-open-icon>
    </div>
    <p>Content text</p>
  </forge-expansion-panel>
</forge-card>
```

## Using the forge-ignore attribute

It is common to place multiple interactive elements within an expansion panel "header" slot. However, you may want to prevent the expansion panel from expanding/collapsing when a specific element is clicked. To do this you can either listen for the click event yourself on the specific elements you care about and call `stopPropagation()` on the event, or you can use the `forge-ignore` attribute for convenience. This attribute is used to prevent the expansion panel from expanding/collapsing when the element (or any children of the element) is clicked.

```html
<forge-expansion-panel>
  <div slot="header" style="display: flex; justify-content: space-between;">
    <button type="button">Toggle Panel</button>
    <!-- 
    Using the forge-ignore attribute allows this element to be placed within the
    expansion panel header without causing the panel to expand/collapse when clicked.
    -->
    <forge-icon-button forge-ignore>
      <forge-icon name="forge_logo"></forge-icon>
    </forge-icon-button>
  </div>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
</forge-expansion-panel>
```

## API

### Properties

| Name | Type | Default | Description |
|------|------|---------|-------------|
| animationType | ExpansionPanelAnimationType | "default" | The type of animation to use when opening/closing the panel. |
| open | boolean | false | Whether the panel is open or closed. |
| orientation | ExpansionPanelOrientation | "vertical" | The orientation of the panel. |
| trigger | string | - | The id of the element that the expansion panel should be toggled by. |
| triggerElement | HTMLElement \| null | - | The element that the expansion panel should be toggled by. |

### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| animation-type | ExpansionPanelAnimationType | "default" | The type of animation to use when opening/closing the panel. |
| open | boolean | false | Whether the panel is open or closed. |
| orientation | ExpansionPanelOrientation | "vertical" | The orientation of the panel. |
| trigger | string | - | The id of the button that the expansion panel is associated with. |

### Events

| Name | Description | Type |
|------|-------------|------|
| forge-expansion-panel-animation-complete | Event fired when the panel has finished animating when toggling. | CustomEvent<boolean> |
| forge-expansion-panel-toggle | Event fired when the panel is toggled open or closed. | CustomEvent<boolean> |

### Slots

| Name | Description |
|------|-------------|
| (default) | The content of the panel. |
| header | The header of the panel. |

### Methods

| Name | Description | Parameters | Return Type |
|------|-------------|------------|------------|
| toggle() | Toggles the open state of the panel. | - | void |

### CSS Custom Properties

| Name | Description |
|------|-------------|
| --forge-expansion-panel-animation-duration | The duration of the open/close animation. |
| --forge-expansion-panel-animation-easing | The easing function of the open/close animation. |

### CSS Shadow Parts

| Name | Description |
|------|-------------|
| content | The content of the panel. |
| header | The header of the panel. |
| root | The root element of the panel. |

## Accessibility

- If the user is able to click the expansion panel to toggle its state, ensure that a `<button>` element is present and clearly labeled to serve as an accessible point of interaction.
- Do not place complex or interactive elements within a button. If your design requires such content in the expansion panel header, place a button in the header alongside that content instead of enclosing it.
- Ensure that the user can focus on the element which activates and deactivates the expansion panel.
- Ensure `aria-expanded` is set on the button to reflect the state of the component. Update it when the panel opens or closes.
- Ensure `aria-controls` is set on the button to reference the id of the expandable content.
- Enclose the expandable content in an element with `role="group"` or another non-generic role.
- Ensure that the expansion panel can be activated by keyboard.

Here is an example of a properly marked up expansion panel:

> **Tip**: A button associated with the expansion panel via `trigger` will automatically have its `aria-expanded` and `aria-controls` values managed.

```html
<forge-expansion-panel trigger="button-id">
  <button slot="header" id="button-id">Toggle panel</button>
  <div id="expandable-content" role="group">Expandable content</div>
</forge-expansion-panel>
```

The button can also be placed elsewhere in the document, outside the expansion panel:

```html
<button id="button-id">Toggle panel</button>
<forge-expansion-panel trigger="button-id">
  <div role="group">Expandable content</div>
</forge-expansion-panel>
```

## CSS-Only

The expansion-panel component is also available as a CSS-only component, but it does require a small amount of JavaScript to toggle the expanded state.

Below is an example JavaScript snippet that toggles the expanded state of the CSS-only expansion panel:

```javascript
// Get the button element
const button = document.querySelector('#my-button');
// Get the expansion panel element
const expansionPanel = document.querySelector('#my-button + .forge-expansion-panel');
// Toggle the expanded state when the button is clicked
button.addEventListener('click', () => {
  const expanded = button.getAttribute('aria-expanded') === 'true';
  button.setAttribute('aria-expanded', !expanded);
  expansionPanel.classList.toggle('forge-expansion-panel--open', !expanded);
});
```

> **Note**: This is a simple example. You may need to adjust the JavaScript to fit your specific use case, or to fit framework-specific usage.

To use the CSS-only expansion panel component, include the following CSS file in your project:

```scss
@use '@tylertech/forge/dist/expansion-panel/forge-expansion-panel.css';
```

### CSS Classes

| Name | Description |
|------|-------------|
| forge-expansion-panel | The expandable element content container (required). |
| forge-expansion-panel__content | The expandable content within the panel container. |
| forge-expansion-panel--open | The open state of the panel. |
