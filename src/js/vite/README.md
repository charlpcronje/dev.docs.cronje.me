---
title: VITE - CRONje.ME
label: VITE
order: 119
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.CRONje.ME/avatars/darker.jpg
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