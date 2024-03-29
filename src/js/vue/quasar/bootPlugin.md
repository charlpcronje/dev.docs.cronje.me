# Create Boot Plugin in Quasar

Quasar `CLI` structures project differently as compared to a standard Vue CLI app. As a result, you cannot just follow examples on the Internets blindly and use `Vue.use()`, or start changing code in `main.js`. There are, however, great ways of addressing the same problems with slightly different solutions.

Enter `boot files`. These were simply called app plugins which led to them being mixed up with Quasar’s own plugins. Now they are simply referred to as “boot files”.

## Why Boot Files?

Use cases for boot files include -

Use common start-up code for your app
Enable functions that are accessible from anywhere
Initialize your own dependencies
A great example is provided out of the box in axios. If you select axios library to be enabled while creating project using Quasar CLI, you will find a boot file in `./src/boot/axios.js.`

```js
import Vue from "vue";
import axios from "axios";

Vue.prototype.$axios = axios;
```

Next, this plugin is registered in `quasar.conf.js.`

```js
module.exports = function (/* ctx */) {
  return {
    boot: ["axios"],
  };
};
```

In any component, you can now do -

```js
const { data } = await this.$axios.get(url);
```

.. without the need to import axios.

## Create a simple boot plugin

The axios plugin works just fine as-is. But, you have no way to provide options in one common place. Take an example of providing just the bearer token -

```js
const { res } = await this.$axios.post(
  `store.state.baseURL/${reqURL}`,
  reqData,
  {
    headers: {
      Authorization: store.state.bearerToken,
    },
  }
);
```

Clutter affects code readability and maintenance - more importantly, we lose “cool” factor.

Let’s create our own version of Axios so that bearer token is included automatically for authentication.

If you are curious - we could always extend the current plugin, but I found it the hard way that it led to confusion for people on the beginner side of spectrum (“axios automatically authenticates in that project, but there is something wrong here”).

```js
Create a new file ./src/boot/req.js.

import axios from "axios";

const req = {
  async post(url, data) {
    try {
      return await axios.post(`https://baseURL.com/${url}`, data, {
        headers: {
          Authorization: "token",
        },
      });
    } catch (e) {
      console.error(e);
    }
  },
};
```json

```js
export default async ({ Vue }) => {
  // something to do
  if (req) req.Vue = Vue;

  Vue.prototype.$req = req;
};
```

> We are doing simple things here

- Create an object with a function
- Create a function within the object that makes axios call with arguments passed to the function
- Register object to be globally available through a Vue prototype
- Register the plugin in quasar.conf.js..

```js
module.exports = function (/* ctx */) {
  return {
    boot: ["req"],
  };
};
```

You can test this code from any component..

```vue
<template>
  <!-- Stuff goes here -->
</template>

<script>
  export default {
    methods: {
      async updateRecord() {
        let reqData = { a: 1, b: 2 };
        const { data } = await this.$req.post("get-sum", reqData);
        console.log("data", data);
      },
    },
  };
</script>
```

## Accessing the Store

Wait, there’s more.

There is no need to hard-code values when you can bring them from one central place - from the Vuex store.

Let’s do that.

```js
Modify ./src/boot/req.js.

import axios from "axios";

export default async ({ Vue, store }) => {
  // something to do
  const req = {
    async post(url, data) {
      try {
        return await axios.post(`${this.store.state.baseURL}/${url}`, data, {
          headers: {
            Authorization: this.store.state.bearerToken,
          },
        });
      } catch (e) {
        console.error(e);
        // throw if you want to pass errors back
      }
    },
  };

  req.Vue = Vue;

  Vue.prototype.$req = req;
};
```

We have included store argument and moved req within the exported function (which was not strictly required, but it avoids creating more variables and confusion with this).

You can now use this.$req.post() from anywhere within your app, and authentication is automatically taken care for you.

Similar to Vue and store, there are other arguments available to your boot function -

## Router

- `ssrContext`: useful in server rendered contexts
- `app`: object that root component instantiates with
