# Layout

You can use the Layout utility to adjust your content based on the user's screen size. Layout returns `'compact'` on mobile devices and at narrow screen widths, and `'regular'` otherwise.

## Implementation

#### Vanilla JavaScript example

```js
import {extend, ExtensionPoint, Text} from '@shopify/admin-ui-extensions';

extend('Admin::Product::SubscriptionPlan::Add', (root, api) => {
  const {layout} = api;
  const currentLayoutText = root.createComponent(Text, {
    children: `The current layout is: ${layout.initialValue.horizontal}`,
  });

  layout.setOnChange((newLayout) => {
    currentLayoutText.updateProps({children: `The current layout is: ${newLayout.horizontal}`});
  });

  root.appendChild(currentLayoutText);
  root.mount();
});
```

#### React example

```js
import {extend, render, useLayout, ExtensionPoint, Text} from '@shopify/admin-ui-extensions';

function App() {
  const layout = useLayout();

  return <Text>{`The current layout is: ${layout.horizontal}`}</Text>;
}

extend(
  'Admin::Product::SubscriptionPlan::Add',
  render(() => <App />),
);
```

## Layout API

`layout`

| Name       | Type                      | Description                                                      | Required |
| ---------- | ------------------------- | ---------------------------------------------------------------- | -------- |
| horizontal | `'regular'`,`'compact'`   | Size of the page.                                                |          |
| setHandler | `(layoutHandler) => void` | Callback to run when the layout changes. Not relevant for React. |          |
