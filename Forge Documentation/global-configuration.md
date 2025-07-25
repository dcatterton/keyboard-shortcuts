# Global Configuration

Tyler Forge provides access to a global configuration object that allows you to override default state for various components that support it. This is useful for setting defaults for your application without having to pass the same properties/attributes to every component instance.

> This feature is currently in preview and is still experimental. It may change in the future, but we welcome feedback on how it can be improved.

## Usage

To use the global configuration object, you will need to ensure you set it up **before** any components are defined. This is typically done as early as possible in your application startup process.

A common place to set up the global configuration object is in your `index.html` file, before any other scripts are loaded.

For example, to set the default label position for all field-based components to `block-start`, you would set the global configuration object as follows:

```javascript
window.TylerForgeGlobalConfiguration = {
  'forge-field': {
    labelPosition: 'block-start'
  }
};
```

The `TylerForgeGlobalConfiguration` object is a simple object where the keys are the component names and the values are objects containing the properties you want to override. The properties you can override are specific to each component and are documented in the component's API documentation.

It's important to note that not all components support global configuration. If a component does not support it, the properties you set in the configuration object will be ignored.

## TypeScript

If you are using TypeScript, Forge ships with ambient type definitions that augment `window` with the `TylerForgeGlobalConfiguration` object.
