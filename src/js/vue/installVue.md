---
title: Install Vue.js | DEVserv.ME
label: Install Vue.js
order: 95
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,vue,js]
---
# Install Vue and it's SFC, CLI

NPM is the recommended installation method when building large scale applications with Vue. It pairs nicely with module bundlers such as `webpack` (opens new window) or `Rollup` (opens new window).

```shell
# latest stable
$ npm install vue@next
```

Vue also provides accompanying tools for authoring `Single File Components (SFCs)`. If you want to use SFCs then you'll also need to install `@vue/compiler-sfc`:

```shell
npm install -D @vue/compiler-sfc
```

If you're coming from Vue 2 then note that `@vue/compiler-sfc` replaces `vue-template-compiler`.

In addition to `@vue/compiler-sfc`, you'll also need a suitable SFC loader or plugin for your chosen bundler. 

In most cases, the preferred way to create a webpack build with minimal configuration is to use Vue CLI.

## CLI

Vue provides an[Official CLI](https://cli.vuejs.org/) (opens new window)for quickly scaffolding ambitious Single Page Applications. It provides batteries-included build setups for a modern frontend workflow. It takes only a few minutes to get up and running with hot-reload, lint-on-save, and production-ready builds

> The CLI assumes prior knowledge of Node.js and the associated build tools. If you are new to Vue or front-end build tools, we strongly suggest going through [the guide](https://v3.vuejs.org/guide/introduction.html) without any build tools before using the CLI.

For Vue 3, you should use Vue CLI v4.5 available on npm as @vue/cli. To upgrade, you need to reinstall the latest version of @vue/cli globally

```shell
yarn global add @vue/cli
# OR
    npm install -g @vue/cli
```

Then in the Vue projects, run

```shell
vue upgrade --next
```
