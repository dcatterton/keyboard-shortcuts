# Theming

Theming within Forge is supported at the core, and colors can be easily adjusted at a granular component level, or across the library as a whole depending on which theme token values are inherited by each component.

All custom theming in Forge is done via adjusting the CSS custom properties, but the library provides utility Sass mixins for every component, as well as the global theme so that you can easily generate the correct custom property definitions. Optionally, you can provide a custom stylesheet that uses the Sass mixins to generate a default set of custom property definitions without needing to override the default definitions if you prefer. More on this below.

An important note about theming is that if you need to customize anything that is not available through CSS custom properties, you can always target internal elements directly using the CSS Shadow Parts.

## Colors

To view a complete set of the color tokens that are available for theming, please view the color design tokens.

## CSS custom properties

If you're not familiar with CSS custom properties, we recommend that you read the MDN documentation before continuing.

CSS custom properties (also known as CSS variables) allow for us to provide custom styles that all components across the library can inherit from for things like global theme values, font size, or any other commonly used CSS value. Along with that, individual components can also define their own custom properties for specific internal styles that are frequently changed. This approach makes sharing styles across the library easier, while giving hooks to specific styles within components that are frequently targeted by developers.

## Overriding global styles

Theming typically begins at adjusting the key colors to match your brand. In the example below you can see that we are setting up a selector targeting the root element, and we're going to override 3 theme values:

```css
:root {
  --forge-theme-primary: hotpink;
  --forge-theme-secondary: blueviolet;
  --forge-theme-tertiary: orangered;
}
```

These theme values are inherited by all components that require these specific color values, but it's important to note that you can also use these values within your own application/components to ensure seamless integration. For example, it is very common to set up your surface and background theme colors for your application:

```css
body {
  background-color: var(--forge-theme-surface-dim);
}

.my-content {
  background-color: var(--forge-theme-surface);
}

.my-custom-class {
  color: var(--forge-theme-primary);
}
```

> Note: the `<body>` styles are defined for you by including the forge-core.css stylesheet for convenience, among a few other important styles.

## Overriding component styles

When you need to override a specific CSS custom property in a specific component instance you will first need to refer to the docs page for the component you care about to see which custom properties are available. From there you can write a selector to target the element:

```html
<forge-card class="my-card"></forge-card>
```

```css
.my-card {
  --forge-card-background: var(--forge-theme-primary);
}
```

## Sass mixins

Using the CSS custom properties directly is always something that you'll need to do, but Forge also provides a robust Sass library that you can take advantage of, especially when it comes to theming and creating your own theme customizations.

Forge provides Sass mixins for developer convenience that allows for providing a key/value Sass map of theme names and style values to override for various component and global theme styles. These mixins are not a requirement to use, but they will make your life easier when it comes to customizing and creating your own themes.

> Forge uses Sass modules. If your project doesn't support Sass modules, you will need to upgrade your installation of sass to make use of these examples.

## Customizing global theme

Forge exposes a mixin called `provide()`, and this allows you to pass in theme names and corresponding color values to use.

In the example below, you will see that we are overriding the `primary`, `secondary`, and `tertiary` theme entries with our custom color values.

```scss
@use '@tylertech/forge/styles/core/styles/theme' as forge-theme;

:root {
  @include forge-theme.provide((primary: red, secondary: green, tertiary: blur));
}
```

This is technically equivalent to writing the following CSS:

```css
:root {
  --forge-theme-primary: red;
  --forge-theme-secondary: green;
  --forge-theme-tertiary: blue;
}
```

The benefit to using the Sass mixin is you get integration with key validation, and can be sure your custom properties will always be generated properly.

## Customizing component theme

Customizing the theme for a specific component can be done much the same way, but you will have to review the documentation for that specific component to know what style hooks it exposes for theming.

In the example below, you'll see that we're overriding component-specific theme values only for the `<forge-badge>` component:

```scss
@use '@tylertech/forge/styles/badge';

.my-custom-badge {
  @include badge.provide-theme((background: red, color: white));
}
```

```html
<forge-badge class="my-custom-badge">Example</forge-badge>
```

## CSS Shadow Parts

If you're not familiar with CSS Shadow Parts, we recommend that you read the MDN documentation before continuing.

Every component that uses Shadow DOM within Forge will also have every element within the internal template marked up with part attributes to enable the use of `::part` selectors to adjust the styles to your needs.

While this customization is available, keep in mind that you are technically overriding the internals of a component. This is not considered part of the public component API and is subject to change between any version. However, changes to internal templates will always be noted in the changelog.

Also, keep in mind that not every component in Forge uses Shadow DOM. There are certain components that rely on global styles. If you see a #shadow-root node when inspecting an element in the browser developer tools then you will know if Shadow DOM is in use.

Many components also make use of slots and the `::slotted` selector. These elements are provided by developers that use content projection to render within a specified slot within the internal component template. These elements are fully customizable by developers when specifying overrides directly using your own selectors.

An example of customizing the internals of a component using CSS Shadow Parts is shown below:

```css
/* Target all <forge-badge> elements and override the "root" shadow part */
forge-badge::part(root) {
  background: red;
  color: white;
}
```

## Dark theme

Forge provides a built-in default dark theme stylesheet for ease of use that complements our default light theme.

A stylesheet is distributed with Forge called `forge-dark.css` this can be found in the npm package under the dist directory.

```scss
@use '@tylertech/forge/dist/forge-dark';
```

Loading this stylesheet in your application (after `forge.css` is loaded) your app will change to dark mode.

The dark theme uses the Sass mixins mentioned above to generate the proper CSS custom property overrides. As you can see below, we just apply the styles to the `:root` selector:

```scss
@use '@tylertech/forge/sass/theme/theme-dark';

:root {
  @include theme-dark.theme-properties;
}
```
