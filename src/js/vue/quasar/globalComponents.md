# Quasar Global Components

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
