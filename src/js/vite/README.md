---
title: VITE - DEVserv.ME
label: VITE
order: 96
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
tags: [dev,js,php,frontend,developer,devtools,prefetch,vite,Preload]
---
## Vite

Vite (opens new window)is a web development build tool that allows for lightning fast serving of code due to its native ES Module import approach.

Vue projects can quickly be set up with Vite by running the following commands in your terminal.

## With npm

```shell
# npm 6.x
npm init vite@latest <project-name> --template vue

# npm 7+, extra double-dash is needed:
npm init vite@latest <project-name> -- --template vue

cd <project-name>
npm install
npm run dev
```

## Or with Yarn:

```shell
yarn create vite <project-name> --template vue
cd <project-name>
yarn
yarn dev
```

Or with pnpm:

```shell
pnpm create vite <project-name> -- --template vue
cd <project-name>
pnpm install
pnpm dev
```