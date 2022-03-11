---
title: UNOCSS | DEVserv.ME
label: UNOCSS 
order: 120
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
tags: [dev,tools,start,frontend,css,developer,devtools,uno,unocss]
---

[UNOCSS Playground](https://unocss.antfu.me/)

The core engine of UnoCSS without any presets. It can be used as the engine of your own atomic CSS framework.

## Usage

```js
import { createGenerator } from '@unocss/core'
const generator = createGenerator({ /* user options */ }, { /* default options */ })
const { css } = await generator.generate(code)
```

## Features

Inspired by `Windi CSS`, `Tailwind CSS`, `Twind` but:

- Fully customizable - no core utilities, all functionalities are provided via presets.
- No parsing, no AST, no scanning, it's INSTANT (200x faster than Windi CSS or Tailwind JIT)
- ~3.5kb min+gzip - zero deps and browser friendly.
- Shortcuts - aliasing utilities, dynamically.
- Attributify Mode - group utilities in attributes
- Pure CSS 
- Inspector - inspect and debug interatively.
- CSS-in-JS Runtime version
- CSS Scoping
- VS Code extension
- Code-splitting for CSS - ships minimal CSS for MPA.
- Library friendly - ships atomic styles with your component libraries and safely scoped

## UnoCSS is designed NOT to be/have

A CSS preprocessor (e.g. @apply) - but you can use shortcuts.
Tailwind's plugin system - but you can write custom rules in seconds and share them as presets!

## Installation

### Vite

```js
npm i -D unocss
```

```js
// vite.config.ts
import Unocss from 'unocss/vite'

export default {
  plugins: [
    Unocss({ /* options */ })
  ]
}
```

Add `uno.css` to your main entry:

```ts
// main.ts
import 'uno.css'
```

See [all packages](https://github.com/antfu/unocss/tree/main/packages)

## Nuxt

```shell
npm i -D @unocss/nuxt
```

```js
// nuxt.config.js

export default {
  buildModules: [
    '@unocss/nuxt'
  ]
}
```

## Configurations

UnoCSS is an atomic-CSS engine instead of a framework. Everything is designed with flexibility and performance in mind. In UnoCSS, there are no core utilities; all functionalities are provided via presets.

By default, UnoCSS applies the default preset. Which provides a common superset of the popular utilities-first framework, including Tailwind CSS, Windi CSS, Bootstrap, Tachyons, etc.

For example, both `ml-3` (Tailwind), `ms-2` (Bootstrap), `ma4` (Tachyons), `mt-10px` (Windi CSS) are valid

```css
.ma4 { margin: 1rem; }
.ml-3 { margin-left: 0.75rem; }
.ms-2 { margin-inline-start: 0.5rem; }
.mt-10px { margin-top: 10px; }
```

Presets
Presets are the heart of UnoCSS that lets you make your own custom framework in minutes.

- Official Presets
  - [@unocss/preset-uno](https://github.com/antfu/unocss/tree/main/packages/preset-uno) - The default preset (right now it's equivalent to @unocss/preset-wind).
  - [@unocss/preset-mini](https://github.com/antfu/unocss/tree/main/packages/preset-mini) - The minimal but essential rules and variants.
  - [@unocss/preset-wind](https://github.com/antfu/unocss/tree/main/packages/preset-wind) - Tailwind / Windi CSS compact preset.
  - [@unocss/preset-attributify](https://github.com/antfu/unocss/tree/main/packages/preset-attributify) - Provides Attributify Mode to other presets and rules.
  - [@unocss/preset-
  - [@unocss/preset-web-fonts](https://github.com/antfu/unocss/tree/main/packages/preset-web-fonts) - Web fonts at ease.
- Community Presets
  - [unocss-preset-typography](https://github.com/ydcjeff/unocss-preset-typography) - Typography Preset by @ydcjeff
  - [unocss-preset-scalpel](https://github.com/macheteHot/unocss-preset-scalpel) - Scalpel Preset by @macheteHot
  - [unocss-preset-chroma](unocss-preset-chroma) - Gradient Preset by @chu121su12

Use Presets

To set presets to your project:

```ts
// vite.config.ts
import Unocss from 'unocss/vite'
import { presetUno, presetAttributify } from 'unocss'

export default {
  plugins: [
    Unocss({
      presets: [
        presetAttributify({ /* preset options */}),
        presetUno(),
        // ...custom presets
      ]
    })
  ]
}
```

When the `presets` option is specified, the default preset will be ignored.

To disable the default preset, you can set `presets` to an empty array:

```ts
// vite.config.ts
import Unocss from 'unocss/vite'

export default {
  plugins: [
    Unocss({
      presets: [], // disable default preset
      rules: [
        // your custom rules
      ]
    })
  ]
}
```

## Custom Rules

Writing custom rules for UnoCSS is super easy. For example:

```css
rules: [
  ['m-1', { margin: '0.25rem' }]
]
```

You will have the following CSS generated whenever m-1 is detected in users' codebase:

```css
.m-1 { margin: 0.25rem; }
Dynamic Rules
To make it smarter, change the matcher to a RegExp and the body to a function:

rules: [
  [/^m-(\d+)$/, ([, d]) => ({ margin: `${d / 4}rem` })],
  [/^p-(\d+)$/, (match) => ({ padding: `${match[1] / 4}rem` })],
]
```

The first argument of the body function is the match result, you can destructure it to get the matched groups.

For example, with the following usage:

```html
<div class="m-100">
  <button class="m-3">
    <
    My Button
  </button>
</div>
```

the corresponding CSS will be generated:

```css
.m-100 { margin: 25rem; }
.m-3 { margin: 0.75rem; }
.p-5 { padding: 1.25rem; }
```

Congratulations! Now you got your own powerful atomic CSS utilities, enjoy!

### Full Controlled Rules

This is an advance feature, you don't need it in most of the cases.
Ordering

UnoCSS keeps the order of the rules you defined to the generated CSS. Later ones come with higher priority.

### Shortcuts

UnoCSS provides the shortcuts functionality that is similar to Windi CSS's

```js
shortcuts: {
  // shortcuts to multiple utilities
  'btn': 'py-2 px-4 font-semibold rounded-lg shadow-md',
  'btn-green': 'text-white bg-green-500 hover:bg-green-700',
  // single utility alias
  'red': 'text-red-100'
}
```

In addition to the plain mapping, UnoCSS also allows you to define dynamic shortcuts.

Similar to Rules, a dynamic shortcut is the combination of a matcher RegExp and a handler function.

```js
shortcuts: [
  // you could still have object style
  {
    'btn': 'py-2 px-4 font-semibold rounded-lg shadow-md',
  },
  // dynamic shortcuts
  [/^btn-(.*)$/, ([, c]) => `bg-${c}-400 text-${c}-100 py-2 px-4 rounded-lg`],
]
```

With this, we could use btn-green and btn-red to generate the following CSS:

```css
.btn-green {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --un-bg-opacity: 1;
  background-color: rgba(74, 222, 128, var(--un-bg-opacity));
  border-radius: 0.5rem;
  --un-text-opacity: 1;
  color: rgba(220, 252, 231, var(--un-text-opacity));
}
.btn-red {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --un-bg-opacity: 1;
  background-color: rgba(248, 113, 113, var(--un-bg-opacity));
  border-radius: 0.5rem;
  --un-text-opacity: 1;
  color: rgba(254, 226, 226, var(--un-text-opacity));
}
```

## Rules Merging

By default, UnoCSS will merge CSS rules with the same body to minimize the CSS size.

For example, `<div class="m-2 hover:m2">` will generate

```css
.hover\:m2:hover, .m-2 { margin: 0.5rem; }
instead of two separate rules:

.hover\:m2:hover { margin: 0.5rem; }
.m-2 { margin: 0.5rem; }
```

## Style Resetting

UnoCSS does not provide style resetting or preflight by default for maximum flexibility and does not populate your global CSS. If you use UnoCSS along with other CSS frameworks, they probably already do the resetting for you. If you use UnoCSS alone, you can use resetting libraries like Normalize.css.

We also provide a small collection for you to grab them quickly:

```js
npm i @unocss/reset
// main.js
// pick one of the following

// normalize.css
import '@unocss/reset/normalize.css'
// reset.css by Eric Meyer https://meyerweb.com/eric/tools/css/reset/index.html
import '@unocss/reset/eric-meyer.css'
// preflights from tailwind
import '@unocss/reset/tailwind.css'
```

Learn more at `@unocss/reset`.

## Custom Variants

Variants allows you to apply some variations to your existing rules. For example, to implement the hover: variant from Tailwind:

```css
variants: [
  // hover:
  (matcher) => {
    if (!matcher.startsWith('hover:'))
      return matcher
    return {
      // slice `hover:` prefix and passed to the next variants and rules
      matcher: matcher.slice(6),
      selector: s => `${s}:hover`,
    }
  }
],
rules: [
  [/^m-(\d)$/, ([, d]) => ({ margin: `${d / 4}rem` })],
]
```

- `match` controls when the variant is enabled. If the return value is a string, it will be used as the selector for matching the rules.
- `selector` provides the availability of customizing the generated CSS selector.

Let's have a tour of what happened when matching for hover:m-2:

- `hover:m-2` is extracted from users usages
- `hover:m-2` send to all variants for matching
- `hover:m-2` is matched by our variant and returns m-2
- the result m-2 will be used for the next round of variants matching
- if no more variant is matched, m-2 will then goes to match the rules
- our first rule get matched and generates .m-2 { margin: 0.5rem; }
- finally, we apply our variants transformation to the generated CSS. In this case, we pre-pended `:hover` to the `selector` hook

As a result, the following CSS will be generated:

```css
.hover\:m-2:hover { margin: 0.5rem; }
```

With this, we could have m-2 applied only when users hover over the element.

The variant system is very powerful and can't be covered fully in this guide, you can check the default preset's implementation to see more advanced usages.

## Extend Theme

UnoCSS also supports the theming system that you might be familiar with in Tailwind / Windi. At the user level, you can specify the theme property in your config and it will be deep merged to the default theme.

```css
theme: {
  colors: {
    'very-cool': '#0000ff',
  },
  breakpoints: {
    xs: '320px',
    sm: '640px',
  }
}
```

To consume the theme in rules:

```css
rules: [
  [/^text-(.*)$/, ([, c], { theme }) => {
    if (theme.colors[c])
      return { color: theme.colors[c] }
  }]
]
```

## Layers

The orders of CSS will affect their priorities. While we will retain the order of rules, sometimes you may want to group some utilities to have more explicit control of their orders.

Unlike Tailwind, which offers fixed 3 layers (base, components, utilities), UnoCSS allows you to define your own layers as you want. To set the layer, you can pass the metadata as the third item of your rules:

```css
rules: [
  [/^m-(\d)$/, ([, d]) => ({ margin: `${d / 4}rem` }), { layer: 'utilities' }],
  // when you omit the layer, it will be `default`
  ['btn', { padding: '4px' }]
]
```

This will make it generates:

```css
/* layer: default */
.btn { padding: 4px; }
/* layer: utilities */
.m-2 { margin: 0.5rem; }
```css

You can control the order of layers by:

```css
layers: {
  components: -1,
  default: 1,
  utilities: 2,
  'my-layer': 3,
}
```

Layers without specified order will be sorted alphabetically.

When you want to have your custom CSS between layers, you can update your entry module:

```js
// 'uno:[layer-name].css'
import 'uno:components.css'
// layers that are not 'components' and 'utilities' will fallback to here
import 'uno.css'
// your own CSS
import './my-custom.css'
// "utilities" layer will have the highest priority
import 'uno:utilities.css'
Utilities Preprocess & Prefixing
UnoCSS also provides the ability to preprocess and transform extracted utilities before processing to the matcher. For example, the following example allows you to add a global prefix to all utilities:

preprocess(matcher) {
  return matcher.startsWith('prefix-')
    ? matcher.slice(7)
    : undefined // ignore
}
```

## Scanning

By default UnoCSS will scan for components files like: `.jsx`, `.tsx`, `.vue`, `.md`, `.html`, `.svelte`, .astro.

`.js` and `.ts` files are not included by default. You can add @unocss-include anywhere in the file that you want UnoCSS to scan at per-file bias, or include *.js or *.ts in the configuration to make all js/ts files as scan targets.

## Inspector

From `v0.7.0`, our Vite plugin now ships with a dev inspector `(@unocss/inspector`) for you to view, play and analyse your custom rules and setup. Visit `http://localhost:3000/__unocss` in your Vite dev server to see it.
