# Design Tokens

Design tokens are the core building blocks of a design system. They are the variables that define the visual design of a product. These variables can be used to define colors, typography, spacing, and much more.

Forge provides a set of design tokens that are used to style the components. These tokens are available as CSS custom properties and can be used to style your own components as well to keep your design consistent and reduce the need to redefine styles.

Design tokens are a powerful tool for creating a consistent design system. They allow you to define the visual design of your product in a single place, and easily reuse those styles throughout your application so that they can be changed dynamically and everything stays in sync.

## Usage

When installing and using Forge, you also have access to a set of global CSS stylesheets that can be loaded into your application. These stylesheets include the design tokens that are used to style the Forge components.

The Forge components do not rely on these tokens being loaded because they are included in the components themselves. However, if you are building your own components, you can use these tokens to style them and this will help keep your application consistent with the Tyler Forge design.

To use the design tokens in your application, you can include the following CSS file in your application:

```css
@use '@tylertech/forge/dist/forge';
```

This will include all of the design tokens that are available in Forge.

If you would like to instead only include specific design tokens, you can include the following CSS file in your application:

```css
// This will load only the theme design tokens
@use '@tylertech/forge/dist/theme/forge-theme';

// This will load only the typography design tokens
@use '@tylertech/forge/dist/typography/forge-typography';

// This will load all other tokens
@use '@tylertech/forge/dist/forge-tokens';
```

To view the tokens in your page, inspect the `<html>` element and look under the `:root` selector.

## Theming

Theming is probably the most common use case for design tokens. By using design tokens, you can easily create a theme for your application that can be changed dynamically. It's important that you use the same theme design tokens as the Forge components so that your application looks consistent with the Forge components, but also adapts to theme changes such as dark mode.

To learn more about theming see the Theming documentation.
