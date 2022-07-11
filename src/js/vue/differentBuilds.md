---
title: Different Builds | CRONje.ME
label: Different Builds
order: 94
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,vue,js]
---

# Explanation of Different Builds

In the `dist/` directory of the npm package (opens new window)you will find many different builds of Vue.js. Here is an overview of which `dist` file should be used depending on the use-case.

## From CDN or without a Bundler

`#vue(.runtime).global(.prod).js:`

- For direct use via `<script src="...">` in the browser, exposes the Vue global.
- In-browser template compilation:
  - `vue.global.js` is the "full" build that includes both the compiler and the runtime so it supports compiling templates on the fly.
  - `vue.runtime.global.js` contains only the runtime and requires templates to be pre-compiled during a build step.
- Inlines all Vue core internal packages - i.e. it's a single file with no dependencies on other files. This means you must import everything from this file and this file only to ensure you are getting the same instance of code.
- Contains hard-coded prod/dev branches, and the prod build is pre-minified. Use the *.prod.js files for production.

> **Note**:  Global builds are not UMD (opens new window)builds. They are built as `IIFEs` (opens new window)and are only meant for direct use via `<script src="...">`.

- `#vue(.runtime).esm-browser(.prod).js`:

- For usage via native ES modules imports (in browser via `<script type="module">`).
Shares the same runtime compilation, dependency inlining and hard-coded prod/dev behavior with the global build.

## With a Bundler

- `#vue(.runtime).esm-bundler.js:`
- For use with bundlers like webpack, rollup and parcel.
- Leaves `prod/dev` branches with process.env.NODE_ENV guards (must be replaced by bundler)
Does not ship minified builds (to be done together with the rest of the code after bundling- )
Imports dependencies (e.g. `@vue/runtime-core`, `@vue/runtime-compiler`)
Imported dependencies are also esm-bundler builds and will in turn import their dependencies (e.g. @vue/runtime-core imports `@vue/reactivity`)
- This means you can install/import these deps individually without ending up with different in-stances of these dependencies, but you must make sure they all resolve to the same version.
- In browser template compilation:
  - `vue.runtime.esm-bundler.js` (default) is runtime only, and requires all templates to be pre-compiled. This is the default entry for bundlers (via module field in package.json) because when using a bundler templates are typically pre-compiled (e.g. in *.vue files).
  - `vue.esm-bundler.js`: includes the runtime compiler. Use this if you are using a bundler but still want runtime template compilation (e.g. `in-DOM` templates or templates via inline JavaScript strings). You will need to configure your bundler to alias vue to this file.

## For Server-Side Rendering

`vue.cjs(.prod).js:`

- For use in Node.js server-side rendering via require().
- If you bundle your app with webpack with target: 'node' and properly externalize vue, this is the build that will be loaded.
- The dev/prod files are pre-built, but the appropriate file is automatically required based on process.env.NODE_ENV.

## Runtime + Compiler vs. Runtime-only

If you need to compile templates on the client (e.g. passing a string to the template option, or mounting to an element using its in-DOM HTML as the template), you will need the compiler and thus the full build:

```js
// this requires the compiler
Vue.createApp({
  template: '<div>{{ hi }}</div>'
})

// this does not
Vue.createApp({
  render() {
    return Vue.h('div', {}, this.hi)
  }
})
```

When using `vue-loader`, `templates` inside `*.vue` files are pre-compiled into JavaScript at build time. You don’t really need the compiler in the final bundle, and can therefore use the runtime-only build.
