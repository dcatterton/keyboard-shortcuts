# Forms

Tyler Forge components are designed to work with forms out of the box. This means that you can use the components within a `<form>` element and they will work as expected.

This has long been a gap in functionality for web components, but with newly available browser APIs we are able to properly allow for our form-associated elements to participate in native form submission and validation.

> Note: This is only available in modern browsers that support the `formAssociated` API for custom elements.

## Form Submission

When using a Forge component within a form, you can expect the component to participate in form submission as you would expect. This means that the component will be able to be submitted with the form and will be included in the form data.

```html
<form>
  <forge-switch name="my-switch">Switch</forge-switch>
  <forge-button type="submit">Submit</forge-button>
</form>
```

In the above example, the `<forge-switch>` component will be included in the form data when the form is submitted.

## Form Validation

Forge components also support form validation. This means that you can use the native form validation APIs to validate the components within a form.

```html
<form>
  <forge-checkbox name="my-checkbox" required>Checkbox</forge-checkbox>
  <forge-button type="submit">Submit</forge-button>
</form>
```

In the above example, the `<forge-checkbox>` component will be required to be checked before the form can be submitted.

## Frameworks

It's important to note that the above examples are using vanilla HTML forms. If you are using a framework like React, Angular, or Vue, you will likely be using a form library that abstracts the form APIs. In these cases, you will need to refer to the documentation for the specific form library you are using to understand how to properly use Forge components within a form.
