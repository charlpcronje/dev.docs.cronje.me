---
Title: Development | CRONje.ME
label: Development - Home
order: 180
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,start,js,php,frontend,backend,developer,devtools,helpers,log]
---
```sh
.__ .___.  ..___.   .__..__ .  ..___.  ..___.   .  ..___
|  \[__ \  /[__ |   |  |[__)|\/|[__ |\ |  |     |\/|[__ 
|__/[___ \/ [___|___|__||   |  |[___| \|  |   * |  |[___
                                                        
```

## Bash Scripting

Bash is not the most exciting topic and I would a very nice reference to most if the issues I've ever experienced: [Bash Scripting](https://www.javatpoint.com/bash-scripting)

## [Dev Tools](./devTools/README.md)

- I created a few development tools that can plug into any `backend` or `frontend` to give me instant `feedback` on any requested `module` / `class`, `method` or `function`
- It is also important to get `feedback` on the `time spend` executing certain tasks.
- Since `PHP 7.4` when they introduced the `PHP RFC: Preload` I saw an opportunity by preloading the `dev tools`, I get to `hook` into any code loaded afterwards, giving me access to monitor any system without interfering with any existing code.

## Some of the tools

- [Getting Started](./devTools/README.md)
- [Console Log Anything](./devTools/consoleLog.md)
- [Error Reporting](./devTools/errorReporting.md)
- [Log Helpers](./devTools/logHelpers.md)
- [Routing](./devTools/route.md)

### 3rd Party MySQL Client

Adminer is a single PHP file web based mysql client, very handy for remote SQL Management

- [Adminer](./devTools/adminer.md)

## Public API's

- [Twillo Public WhatsApp API](./api/twillo.md)

## Chrome Extensions

- [Manifest V3](./chromeExt/manifestV3.md)
- [Options Page](./chromeExt/optionsPage.md)

## Frontend Development

- [Prototyping](./html/prototyping.md)
- [Preloading & Prefetching](./html/prefetchAndPreload.md)
- [Themes & Design](./html/themesAndDesign.md)
- [UNOCSS](./html/unocss.md)
- [CSS Grid](https://www.youtube.com/watch?v=0xMQfnTU6oo)

### JavaScript

- [GraphQL](./js/graphql/README.md)
- [GraphQL & Axios](./js/graphql/axios.md)
- [Cash.js](./js/libs/cash-js.md)

### Node.js - Server Side Scripting

- [Node Version Manager](./node/nvm.md)
- [Creating a node.js Cmd Line App](./node/nodecli.md)

### JS Libraries

- [Cash JS](./js/libs/cash-js.md)
- [jsDoc](./js/libs/jsDoc.md)
- [PReact](./js/libs/PReact.md)
- [jsMVC](./js/libs/jsMVC.md)
- [GreenSock 'GSAP'](./js/libs/gsap.md)
  - [Simple Example](https://www.youtube.com/watch?v=m6PDUIF24v4)

### JS Document Editors, Mockups and Site Generators

- [Blocks UI](blocksui.md)
- [Gatsby + Netlify CMS Starter](https://github.com/ritesh2204/gatsby-starter-netlify-cms)
- [Grapes.JS Block Website Dev](grapesjs.md)
- [Kadence Blacks Web Builder](https://cloud.kadenceblocks.com/)
- [SlateJS](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/)
  - [Slate on GitHub](https://github.com/smashingmagazine/wysiwyg-editor)
- [SlateJS Examples](slatejs/README.md)
- [Plate Editor Playground](https://codesandbox.io/s/2mh1c)

### Code sandbox

- [Code Sandbox Client](https://github.com/codesandbox/codesandbox-client)
- [GrapesJS Examples](https://codesandbox.io/examples/package/grapesjs)
- [GrapesJS Block (Good)](https://codesandbox.io/s/lej2t?file=/src/index.js)
- [GrapesJS Newsletter](https://codesandbox.io/s/urxqy?file=/src/App.js)]
- [GrapesJS MicroSite Builder](https://codesandbox.io/s/o9hxu)
- [Tailwind CSS](https://codesandbox.io/examples/package/tailwindcss)
- [Tailwind Dropdown with group-hover](https://codesandbox.io/s/gm9k9)
- [Dark Mode Tailwind](https://codesandbox.io/s/ndpw4)
- [Subscribe To Our Newsletter](https://codesandbox.io/s/r3wu9?file=/src/index.js)
- [React Table](https://codesandbox.io/s/sw030?file=/src/App.js)
- [Nuxt starter](https://codesandbox.io/s/h0z15)

### Vue.js Framework

- [Vue.js](js/vue/README.md)
- [Install Vue and it's SFC, CLI](./js/vue/installVue.md)
- [Different Builds](./js/vue/differentBuilds.md)
- [Composition API](./js/vue/composition/api.md)
- [Fetching Data](./js/vue/composition/fetchData.md)
- [Vue Web Storage](./js/vue/vueWebStorage.md)

### Quasar JS Frameworks  

- [Quasar](./js/quasar/README.md)
- [Command List](./js/quasar/commandList.md)
- [Global Components](./js/quasar/globalComponents.md)
- [Boot Files](./js/quasar/bootFiles.md)
- [Boot Plugin](./js/quasar/bootPlugin.md)
- [Quasar Pre-fetch](./js/quasar/quasarPrefetch.md)
- [Quasar Assets](./js/quasar/quasarAssets.md)
- [API Proxy](./js/quasar/apiProxy.md)
- [Sass in JS](./js/quasar/sassInJs.md)
- [env Process](./js/quasar/envProcess.md)
- [Deploying Or Building](./js/quasar/deployingOrBuilding.md)
- [Quasar Testing](./js/quasar/quasarTesting.md)
- [Dev For Public](./js/quasar/devForPublic.md)

### State Management

- [Custom State Management](customState.md)

### Build Tools

- [Vite](./js/vite/README.md)

## Perl Development

- [Getting started with Perl](perl/gettingStarted.md)
- [Perl Scripting IDE's](perl/perlIDEs.md)
- [Argument Parsing Sub-Routines](perl/argsSubRoutines.md)
- [Dots in Perl](perl/dotsInPerl.md)
- [Singletons](perl/singleton.md)
- [Static Variables](perl/staticVars.md)
- [Variable variables](perl/variableVariables.md)

### Perl Libraries

- [Hash.Digger](perl/libs/Hash.Digger.md)
- [Class.Tiny](perl/libs/Class.Tiny.md)
- [Config.Tiny](perl/libs/Config.Tiny.md)
- [HTML.Tiny](perl/libs/HTML.Tiny.md)
- [Path.Tiny](perl/libs/Path.Tiny.md)
- [Set.Tiny](perl/libs/Set.Tiny.md)
- [SQL.Tiny](perl/libs/SQL.Tiny.md)
- [XML.Tiny](perl/libs/XML.Tiny.md)

### Perl Regular Expressions

- [Regex Basics](perl/regex/regexBasics.md)
- [Regex for SSH Agent](perl/regex/regexForSSHAgent.md)
- [Sample Data](perl/regex/sampleData.md)
- [Sub Strings](perl/regex/subStrings.md)
- [Regex in Perl](perl/regex.md)

## PHP Development

- [PHP](./php/README.md)
- [Preload](./php/preload.md)
- [Laravel](./php/laravel/README.md)
- [Laravel CORS](./php/laravel/cors.md)
- [Run shell_exec as sudo](./php/shellExec/README.md)

## RStudio IDE

- **[R Programming](./rLang/README.md)**
  - [Awesome R](./rLang/awesomer.md)
  - [Install R](./rLang/installR.md)
  - [R Studio](./rLang/rstudio.md)
- **[R Markdown](./rLang/rmd.md)**
  - [Markdown Templates](./rLang/mdTemplates.md)
  - [Portfolio Template](./rLang/cvTemplare.md)
  - [Quarto guide](./rLang/quartoGuide.md)
- **[Web-Scraping](./rLang/webScraping.md)**

## Icon Sets

- [octIcons](./icons/octIcons.md)  
- [Material Design Icons](./icons/materialIcons.md)
  