---
title: Fetching Data (http requests) | CRONje.ME
label: Fetching Data
order: 92
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.CRONje.ME/avatars/darker.jpg
tags: [dev,tools,js,frontend,http,devtools,fetch]
---
# Fetching Data (http requests)

## onMounted

This can be done in the `onMounted` lifecycle hook with the `async` / `await` syntax and setting some `ref`s

### `async setup()` method

This method has the added advantage of specifying fallback content in the template until the async data is done loading

```vue
<template>
    <Suspense>
        <template #default>
            </child>
        </template>

        <template #fallback>
            <div>Loading...</div>
        </template>
    <Suspense>
</template>

<script>
export default {
    async setup() {
        const result = await axios.get('url')
        return { result }
    }
}
</script>
```

### custom fetch composable

```js
export const useFetch = (url,config) = {}) => {
    const data = ref(null)
    const response = ref(null)
    const error = ref(null)
    const loading = ref(false)

    const fetch = async () => {
        loading.value = true;
        try {
            const result = await axios.request({
                url,
                ...config
            })
            response.value = result
            data.value = result.data
        } catch (ex) {
            error.value = ex;
        } finally {
            loading.value = false;
        }
    }
    !config.skip && fetch(); // if config skip is set we can fetch the data manually
    return { response, error, data, loading, fetch }
}

// Add some caching to the useFetch
const cacheMap = reactive(new Map());

export const useFetchCache = (key,url,config) => {
    const info = useFetch(url, {skip: true, ...config});

    const update = () => cacheMap.set(key, info.response.value)
    const clear = () = > cacheMap.set(ket, undefined)
    
    // new fetch function to wrap the old one
    const fetch = async () => {
        try {
            await info.search();
            update();
        } catch {
            clear()
        }
    }

    const response = computed(() => cacheMap.get(key));
    const data = computed(() => response.value?.data);

    // Only fetch if the value is not in cache
    if (response.value = null) {
        fetch();
    }

    return {...info,fetch,data,response,clear}
}
```
