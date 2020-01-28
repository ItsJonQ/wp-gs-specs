# Global Styles - Style Schema

> WIPWIPWIP

A Style `schema` represents the data structure for an individual global style or group.

## Groups

A **group** is a collection of related styles.

In the following example, there are several groups that branch from the primary "global" collection:

```sh
global-styles
  └── global
      ├── color
      └── typography
```

`global` in this context refers to base styles that are **not block specific**.

This can be represented by a JSON object that resembles:

```js
{
  "color": { ... },
  "typography": { ... },
}
```

Block styles can also have groups, under the key of "blocks" rather than "global".

```sh
global-styles
  ├── global
  │   ├── color
  │   └── typography
  └── blocks
      ├── core/paragraph
      └── ...
```

### Group Schema

By default, core will provide the following data structure:

```sh
global-styles
  ├── global
  │   ├── color
  │   └── typography
  └── blocks
```

The above groups and namespaces will **always** exist.

The following represents the data of the `color` group:

```ts
type GlobalStylesGroup = {
  name: string;
  title: string;
};

// Example of a color group
const colorGroupSchema = {
  name: "global/color",
  title: "Color"
};
```

**name**:
The unique (slug) name of the group. The value before the `/` determines which group to add this group to.

**title**:
The visible title of the group. This is seen within the UI of the Global Styles editor.

## Styles

A style is an individual entry within the global style groups.

### Style Schema

```ts
type GlobalStylesStyleType =
  | "boolean"
  | "color"
  | "range"
  | "number"
  | "select"
  | "text";

type GlobalStylesStyle = {
  name: string;
  title: string;
  defaultValue: string | number;
  type: GlobalStylesStyleType;
};

// Example of a color style for "text"
const globalColorStyle = {
  group: "global",
  name: "color/text",
  title: "Text Color",
  defaultValue: "#000000",
  type: "color"
};
```

**group**:
Refers to the groups to add this style to.

**name**:
The unique (slug) name of the style.

**title**:
The visible title of the style. This is seen within the UI of the Global Styles editor.

**defaultValue**:
The initial value of the style. This value will be used if a user customized global style is resetted.

**type**:
Determines the (generated) Control UI within the Global Styles editor.

## Registering custom styles

In the following example, we'll walk through how one would register a custom global style.

Let's say we'd like to register custom `font-pairing` values, which will be used in several of our custom Gutenberg blocks.

### Custom global style

First, we'd need to register our global `font-pairing` group:

```js
const globalFontFamilyPairing = {
  name: "global/font-pairing",
  title: "Font Pairing"
};

registerGlobalStylesGroup(globalFontFamilyPairing);
```

(Note: The `registerGlobalStylesGroup` function is sudo code)

The global styles scheme will now look like this:

```sh
global-styles
  ├── global
  │   ├── color
  │   ├── font-pairing
  │   └── typography
  └── blocks
```

Next, we'll add a couple of values to our `font-pairing` group:

```js
const globalFontHeading = {
  group: "global",
  name: "font-pairing/heading",
  title: "Heading Font",
  defaultValue: "Helvetica",
  type: "text"
};

const globalFontHeading = {
  group: "global",
  name: "font-pairing/body",
  title: "Body Font",
  defaultValue: "Georgia",
  type: "text"
};

registerGlobalStyles(globalFontHeading);
registerGlobalStyles(globalFontBody);
```

(Note: The `registerGlobalStyles` function is sudo code)

The global styles scheme will now look like this:

```sh
global-styles
  ├── global
  │   ├── color
  │   ├── font-pairing
  │   │   ├── heading
  │   │   └── body
  │   └── typography
  └── blocks
```

Note: The `font-pairing` group is sorted alphabetically. Whereas the items under the `font-pairing` group are sorted based on order of registry.

The above global styles schema would result in CSS variables that look like the follow (below), which provide the rendered values for our custom block's CSS.

```sh
:root {
  ...
  --wp-gs-font-pairing-heading: Helvetica;
  --wp-gs-font-pairing-body: Georgia;
  ...
}
```

### Custom block style

Let's say we have a custom `my-custom-blocks/fonts` block. In this block, we'd like to register a custom global style, dedicated to this block, which will look like:

```js
// my-custom-blocks/font.js
const myCustomBlocksFontStyles = {
  group: "my-custom-blocks",
  name: "color/text",
  title: "Text Color",
  defaultValue: "#000000",
  type: "color"
};

registerGlobalBlockStyles(myCustomBlocksFontStyles);
```
