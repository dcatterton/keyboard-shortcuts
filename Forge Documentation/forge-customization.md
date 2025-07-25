# Customization

There are many ways that Forge components can be customized. Whether you are looking for theming, overriding internal styles within the Shadow DOM, or looking to extend a component with new functionality you will find information about how to go about that within this guide.

## Theming

All components within Forge support theming at the core. To view detailed information about theming, please view the [theming guide](#).

## CSS

When attempting to customize a component via CSS, you will be using either [CSS Custom Properties](#) or [CSS Shadow Parts](#). Both of these CSS-based solutions will give you access to changing how the internals of a component are rendered without adjusting any functionality.

For example, Forge provides many CSS custom properties from within specific components to help adjust specific internal styles:

```css
forge-button {
  --forge-button-background: red;
}
```

If you want to have complete control over any of the internal styles within a component, that's where CSS Shadow Parts come in. This feature allows you to target any named "part" of a component (any element within the components' Shadow DOM that has a `part` attribute applied) and set any CSS styles on it that you wish:

```css
forge-button::part(root) {
  height: 100px;
  background-color: red;
  display: grid;
}
```

## HTML

You can also customize components via HTML using the provided HTML [slot](#) elements within the Shadow DOM of a component. This allows for you to project your own content into specifically named locations within the internal template of a component. Typically a component will expect certain elements to be applied within these slots, but this also allows for you to potentially customize the usage to your needs if you see fit.

```html
<forge-text-field>
  <label for="input">Label</label>
  <input type="text" id="input" />

  <!-- Render a custom element into a slot if desired -->
  <forge-badge slot="helper-text">Custom helper text</forge-badge>
</forge-text-field>
```

So as you can see, you can customize anything you want. Now, would you typically want to do that? Probably not since it doesn't follow proper design guidance, but these examples show you how you might be able to customize things and how easy that can be achieved.
