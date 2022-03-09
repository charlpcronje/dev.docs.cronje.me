---
icon: file-zip
expanded: true
title: Quasar Global Components | DEVserv.ME
label: Global Components
order: 65
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
date: 2022-01-25
tags: [dev,tools,js,frontend,backend,devtools,quasar,global,components]
---

## Create new Boot file

```shell
quasar new boot RegisterGlobalCOmponents
```

## Update `quasar.conf.js`

```js
boot: [
    'RegisterGlobalCOmponents',
],
```

## Create new component

```shell
quasar new component globalComponent
```

## Update Boot file

Edit `RegisterGlobalCOmponents.js` in the `/src/boot` folder

```js
import { boot } from 'quasar.wrappers` 
import globalComponent from  'components/globalComponent.vue'

export default boot(async ({ app }) => {
    app.component('globalComponent',globalComponent);
});
```
