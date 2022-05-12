---
title: Vue.js Composition API | CRONje.ME
label: Composition API
order: 93
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,vue,js]
---
## watch Effect

> Watch Effect will be executed every time any one of the dependencies of the variable changes

```js
export default {
    setup() {
        const count = ref(0);

        watchEffect(()=> {
            console.log('Value of count: {count.value}');
        });
        return { count }
    }
} 
```

## watch

> Also watches a ref and gives you access to the current and prev value. You can watch a rer directly or a getter of a ref
> watch an take a ref or an array of refs

```js
export default {
    setup() {
        const counter = reactive({ count: 0 })
        watch(
            () => counter.count,
            (curr,prev) => {/** dostuff **/}
        ) 

        const count = ref(0
        watch(
            count,
            (curr,perv) => {/** dostuff **/}
        )
    }
}
```

## Lifecycle hooks

> One example of a lifecycle hook is the `onMounted` function
