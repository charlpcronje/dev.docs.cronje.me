---
icon: pulse
expanded: true
title: Vue Web Storage | DEVserv.ME
label: Vue Web Storage
order: 50
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,vue,js]
---

## Features

- Choose either localStorage or sessionStorage or both
- Prefix all of your stored keys
- Auto JSON.stringify and JSON.parse
- Events for cross tab communication

## Install

```shell
# yarn
yarn add vue-web-storage
```

## Usage

The usage is a bit different than the online docs, whe have to import it via a boot file

So first create a new `boot` file

```shell
quasar new boot viewWebStorage
```

Edit Boot File `/src/boot/viewWebStorage.js`

```json
import { boot } from 'quasar/wrappers'
import StoragePlugin from 'vue-web-storage';


export default boot(({ app }) => {
  app.use(StoragePlugin, {
    prefix: 'secZone_',// default `app_`
    drivers: ['session', 'local'], // default 'local'
  });

  // It will register two different instances
  // this.$sessionStorage
  // this.$localStorage
});
```

## Methods

All methods take care of prefix in key name, so you no need to specify the prefix when using them.

`set(key,value)`

Stores the value under specified key in storage. Convert value to JSON before saving. This method throws error on failure.

```js
this.$localStorage.set('name', 'john')
this.$localStorage.set('isAdmin', true)
this.$localStorage.set('roles', ['admin', 'sub-admin'])
this.$localStorage.set('permission', {id: 2, slug: 'edit_post'})
```

`get(key, ?defaultValue = null)`

Retrieves given key value from storage, parse the value from JSON before returning. If parsing failed then throws error.

```js
this.$localStorage.get('name')
this.$localStorage.get('doesNotExistsInStorage', 'defaultValue')
```

`remove(key)`

Removes the individual key from storage.

```js
this.$localStorage.remove('name')
```

`clear(?force = false)`

Removes all keys from storage. Passing true will clear whole storage without taking prefix into consideration.

```js
this.$localStorage.clear()
```

`keys(?withPrefix = false)`

Returns array of keys stored in storage. Passing true will return prefixed key names.

```js
this.$localStorage.keys()
```

`hasKey(key)`

Returns true if key exists in storage regardless of its value.

```js
this.$localStorage.hasKey('name')
```

`length()`

Returns the number of keys stored in storage.

```js
this.$localStorage.length()
```

Events
💡 These are not regular Vue.js events, these events to be used for cross tab communication.
`on(key,fn)`

Attaches a listener method to the given key. You can attach multiple methods on the same key.

```js
const onChangeName = (newValue, OldValue, originUrl) => {
    // do something when `name` value gets changed
};
this.$localStorage.on('name', onChangeName);
this.$localStorage.on('name', this.anotherMethod)
```

`off(key,fn)`

Removes specified listener method form the given key.

```js
this.$localStorage.off('name', this.onChangeName)
```

`clearEvents(?key)`

Removes all listeners for the given key otherwise clears the listeners pool when key not specified.

```js
this.$localStorage.clearEvents('name');
this.$localStorage.clearEvents()
```

## Install in non-module environments (without webpack)

```html
<!-- Vue js -->
<script src="https://cdn.jsdelivr.net/npm/vue@3"></script>
<!-- Lastly add this package -->
<script src="https://cdn.jsdelivr.net/npm/vue-web-storage@6"></script>
<!-- Init the plugin -->
<script>
    yourApp.use(VueWebStorage.default)
</script>
```
