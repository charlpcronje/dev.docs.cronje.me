---
itle: Quasar | CRONje.ME
label: Quasar
order: 93
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,start,js,php,frontend,backend,developer,devtools,helpers,log]
---

## Getting Started

- [Command List](./commandList.md)
- [Boot Files](./bootFiles.md)
- [Boot Plugin](./bootPlugin.md)
- [Quasar Pre-fetch](./quasarPrefetch.md)
- [Quasar Assets](./quasarAssets.md)
- [Quasar Global Comments](./globalComponents.md)
- [API Proxy](./apiProxy.md)
- [Sass in JS](./sassInJs.md)
- [env Process](./envProcess.md)
- [Deploying Or Building](./deployingOrBuilding.md)
- [Quasar Testing](./quasarTesting.md)
- [Dev For Public](./devForPublic.md)

## Why Quasar?

Zero configuration features

- Cache busting
- Tree Shaking
- Lazy Loading
- ES6 Transpiling
- Code Linting
- One Code Base

## Cache Busting

Cache busting is the process of uploading a new file to replace an existing file that is already cached. This is useful because the cache will often take a long time to expire from all of its various locations and cache busting properly ensures that any changes to a file be visible to end users sooner, rather than later.

## Tree Shaking

Tree shaking is a term commonly used within a JavaScript context to describe the removal of dead code.

It relies on the import and export statements in ES2015 to detect if code modules are exported and imported for use between JavaScript files.

In modern JavaScript applications, we use module bundlers (e.g., webpack or Rollup) to automatically remove dead code when bundling multiple JavaScript files into single files. This is important for preparing code that is production ready, for example with clean structures and minimal file size.

## Lazy Loading

Lazy loading is the practice of delaying load or initialization of resources or objects until they're actually needed to improve performance and save system resources. ... Reduces initial load time – Lazy loading a webpage reduces page weight, allowing for a quicker page load time.

## ES6 Transpiling

While support for ES6 is always increasing, we can’t always assume that users will be using a browser that supports all its features. So, in order to utilize ES6 features now and make sure we won’t run into cross-browser compatibility issues, we need to transpile our code.

## Code Linting

Linting is the automated checking of your source code for programmatic and stylistic errors. This is done by using a lint tool (otherwise known as linter). A lint tool is a basic static code analyzer.

Linting is important to reduce errors and improve the overall quality of your code. Using lint tools can help you accelerate development and reduce costs by finding errors earlier.

## One Code Base

Being able to write code once and compile the application on all devices means more than what is sounds. By not having 2 or 3 different set of code to maintain you save on:

- Initial dev time and cost
- Maintenance
- Lets the developers skill up more focused
- Updates ad upgrades all happen at the same time on all platforms
- The users get the same app no matter the device
- Documentation is also now one set documents

## Underlying Technologies

- Vue
- Node.js
- WebPack
- Cordova
- Capacitor
- Electron
