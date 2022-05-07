---
title: Use Sass Variables in Javascript | CRONje.ME
label: Sass Variables in JS
order: 80
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://charl-cv.CRONje.ME
    avatar: https://assets.CRONje.ME/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,quasar,sass]
---

Sass variables are awesome in that they guarantee that you are using the right colors, dimensions, animations but it proved to be difficult to implement.

## Install

```shell
yarn add --dev node-sass-json-importer
```

## Update `quasar.conf.js`

```js
const jsonImporter = require('node-sass-json-importer')
module.exports = function (ctx) {
  return {
    ...
    build: {
      ...
      sassLoaderOptions: {
        sassOptions: {
          importer: jsonImporter()
        }
      }
    }
  }
}
```

## Create variables

You can save your settings as JSON in `src/css/quasar.variables.json`. remember not to repeat these keyValues in your real SASS file.

```json
{
    "primary": "#3215B3",
    "secondary": "#29269A",
    "accent": "#9C27FF",
    "info": "#3100EC",
    "spotColor": "#C0FF33"
}
```

## Update your SASS file

Replace your `src/quasar.variables.sass` with the following:

```js
@import "./quasar.variables.json"
```

## Create and register a boot file `src/boot/sass.js`

```js
import sass from '../css/quasar.variables.json'

export default ({ Vue }) => {
  Vue.prototype.$sass = sass
}

export { sass } // in case you need it outside of vue
```

## Use your sass variable in a Vue Component

```js
methods: {
    sassColor (colorName) {
      return this.$sass[colorName]
    },
    sassSpotColor () {
      return this.$sass['spotColor']
    }
  }
```

This method of getting new things available in your app with the this.$abc will work with a lot more than just this example
