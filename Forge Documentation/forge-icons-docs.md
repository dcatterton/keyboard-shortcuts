# Icons

Tyler Forge provides a set of icons that can be used in your application and libraries. These icons are SVGs and can be used either directly in your HTML or more commonly via the Forge icon component.

To learn more about the Forge icon component, see the [documentation](#).

## Icon Library

Icons are distributed via the Tyler icons library. This library is made up 3 sets of icons:

- **Standard**: The standard Material Design icons.
- **Extended**: This is a subset of the community-based Material Design icon set.
- **Custom**: Custom icons created by Tyler Technologies.

These three sets of icons are combined into a single library that can be used in your applications, that gives you access to over 5000 icons.

> Note: we are currently in the planning phase of combining all 3 icon sets into a single library to reduce confusion and deduplication of the icons. This will be available in a future release. See the roadmap to view the status of this project.

You can view the full set of icons or search the library in the design system [here](#).

## Installation

The Tyler icons library is available as an NPM package, or from the Forge CDN.

### NPM Package

This is the recommended way to consume icons in your applications or libraries. You can install the package using the following command:

```bash
npm install @tylertech/tyler-icons
```

## Usage

The icons are distributed as ES modules, so you can import them directly into your application:

```javascript
import { tylIconFavorite } from '@tylertech/tyler-icons/standard';
import { tylIconHeart } from '@tylertech/tyler-icons/extended';
import { tylIconForgelogo } from '@tylertech/tyler-icons/custom';
```

Each icon object consists of a `name` and `data` property. The `name` is the name of the icon, and the `data` is the raw SVG string for the icon.

Each icon can then be registered for use with the `<forge-icon>` component using the `IconRegistry`:

```javascript
import { IconRegistry } from '@tylertech/forge';

IconRegistry.define([tylIconFavorite, tylIconHeart, tylIconForgelogo]);
```

You can then use the icon in your HTML like so:

```html
<forge-icon name="favorite"></forge-icon>
<forge-icon name="heart"></forge-icon>
<forge-icon name="forge-logo"></forge-icon>
```

## CDN

You can also access the icons directly from the CDN as `.svg` files. This is useful if you want to use the icons as images instead, or fetch the icons manually.

### Image

```html
<img src="https://cdn.forge.tylertech.com/v1/icons/svg/standard/cake.svg" alt="Cake icon" />
```

> Note: Make note of the "standard" part of the URL. This is the icon set that the icon belongs to. You can replace this with "extended" or "custom" to access icons from those sets.

### Fetch

You could also fetch these SVG files dynamically in your application using the `fetch` API. This would give you access to the `<svg>` data that you could then render in your HTML. In fact, this is exactly what the `<forge-icon>` component does under the hood:

```javascript
fetch('https://cdn.forge.tylertech.com/v1/icons/svg/standard/cake.svg')
  .then(response => response.text())
  .then(svgCode => {
    // Use the SVG in your HTML
  });
```

## Contribution

The icon library is hosted on GitHub and is open source. If you would like to view the source code or contribute to the library, you can find the repository here: https://github.com/tyler-technologies-oss/tyler-icons

Tyler Technologies uses the Material Design Icons as a base for the standard and extended icon sets. These icons are licensed by Google but self-hosted by Forge to ensure availability and performance. We do not modify the icons in any way, and they are distributed under the original licensing terms.

The custom icons are created by Tyler Technologies and are licensed under Apache 2.0.
