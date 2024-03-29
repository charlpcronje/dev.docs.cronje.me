# @quasar/testing

> You're looking at Quasar v1 testing docs. While AEs migration to support Quasar v2 is in progress, you can find the documentation for Quasar v2 versions [here](https://github.com/quasarframework/quasar-testing/tree/next)
>
> Check out the migration status [here](https://github.com/quasarframework/quasar/discussions/10341)

This is the monorepo for integrating the test-runner of your choice into your Quasar app.

You can install multiple pre-rigged testing harnesses (test runners) to your Quasar application, each one will:

- install the harness NPM package into your project;
- scaffold necessary configuration files;
- add script commands, if you so choose, which expose some functionality of the respective harness.

> App Extensions (such as these testing harnesses) only work with Quasar CLI, not with Vue CLI, nor by directly installing packages via a package manager as npm or yarn. Use `quasar ext add ...` or the installation step won't be executed and configuration files won't be copied over.

Testing is not in and of itself hard. The most complicated part is setting up the testing harness. The trick lies in knowing what to test. If you are new to testing, it is absolutely imperative that you familiarize yourself with some of the concepts and patterns. There are some links for further reading at the end of this document page.

The Test Driven Design approach will help you to write better (and fewer) tests. Even though it may seem like it slows you down to some degree, this habit pays its dividends on the long term drastically reducing the number of public bugs and the project maintenance effort. Think of tests like insurance for your code that always pays out. On the other hand, not everything is worth being tested, or is worth being tested only at an higher level (eg. using an E2E tests instead of unit tests).

> REMEMBER
> Test the functionality, not the function</div>

## Table of contents

- [@quasar/testing](#693-quasartesting)
  - [Table of contents](#table-of-contents)
  - [Donations](#donations)
  - [Installation](#installation)
  - [Removal](#removal)
  - [Reset](#reset)
  - [Upgrade](#upgrade)
    - [Upgrade to a new major version with NPM](#upgrade-to-a-new-major-version-with-npm)
  - [Testing Harnesses Manager](#testing-harnesses-manager)
  - [Unit Testing](#unit-testing)
    - [Jest](#jest)
    - [AVA **DEPRECATED**](#ava-deprecated)
  - [e2e Testing](#e2e-testing)
    - [Cypress](#cypress)
    - [WebDriver.io (wdio) **DEPRECATED**](#webdriverio-wdio-deprecated)
    - [Quality Auditing](#quality-auditing)
  - [Contributing](#contributing)
  - [Road map](#roadmap)
    - [UNIT](#unit)
    - [E2E](#e2e)
    - [QUALITY](#quality)
    - [UTILS](#utils)

## Donations

The Quasar team spend a considerable amount of time studying, coding and maintaining App Extensions which save literally thousands of developers hours, days or weeks of work.

Does your business or personal projects depend on these App Extensions? How much time did we save you until now? Consider [donating](https://github.com/sponsors/rstoenescu) to help us maintain them and allow us to create new ones!

## Installation

You can add test harnesses:

- in a centralized way via the [Testing Harnesses Manager](packages/testing/README.md);
- using an "a-la-carte" approach, checking each harness documentation.

You can add multiple harnesses and even use them into your continuous integration pipelines.

## Removal

You can remove a testing harness running:

```shell
quasar ext remove @quasar/testing-unit-jest
```

This will remove the associated NPM package and run the Quasar App Extensions uninstall hook.
If not done into the AE uninstall hook, the removal won't delete test or configuration files.

## Reset

If you mess up your configuration and need to reset, or just want to check out if there has been any changes into new versions configuration, you should run:

```shell
quasar ext add @quasar/testing-unit-jest
```

Be careful though, this will overwrite ALL existing files (including configurations) if you allow it to. Make sure to have some kind of version control in place before proceeding. This operation will also upgrade the NPM package and its dependencies.

To prevent installing new or updated dependencies, you should run:

```shell
quasar ext invoke @quasar/testing-unit-jest
```

## Upgrade

You can upgrade a testing harness and its dependencies by updating its related NPM package.

```shell
yarn add -D @quasar/quasar-app-extension-testing-unit-jest
```

This won't change existing test or configuration files.

### Upgrade to a new major version with NPM

When upgrading between major versions, since there are major changes, we suggest you to remove and re-add the AE, to obtain latest configuration files too.
Ensure your source control is clean before proceeding, then answer (y) and "Overwrite all" when prompted to overwrite existing files and individually `git diff` all changes manually to check out which changes you want to keep and which you want to revert.

```shell
quasar ext remove @quasar/testing-unit-jest
quasar ext add @quasar/testing-unit-jest
```

## Testing Harnesses Manager

[Check out Testing Harnesses Manager AE documentation](packages/testing/README.md)

## Unit Testing

### [Jest](https://jestjs.io/)

[Check out Jest AE documentation](packages/unit-jest/README.md)

### [AVA](https://github.com/avajs/ava) **DEPRECATED**

> You're looking at Quasar v1 AVA AE docs. This AE has been deprecated and won't be migrated to support Quasar v2, you can find the announcement [here](https://github.com/quasarframework/quasar/discussions/10341)

```shell
 quasar ext add @quasar/testing-unit-ava
```

We have included:

- a configuration file `ava.config.js`
- `/test/ava/setup.js`
- `babel.config.js` file
- a `quasar` scaffolding helper
- a 'validity' test that makes sure quasar is initiatable

We have included the optional ability to place your test code inside your vue files, should you choose to do so. It will be rendered by webpack HMR. To run these tests, run `$ quasar test --unit ava --dev`.

```html
<test lang="ava">
  /* your complete test file here */
</test>
```

> You may notice that your IDE doesn't know how to parse the test block, so go into the `<test/>` block, press `<alt> + <enter>`, select 'inject language or reference' and select `javascript`. This will grant `<test/>` blocks autocomplete.

## e2e Testing

We recommend testing webapps with Cypress if you target Chrome-based browsers (Chrome, Edge, Electron) or Firefox - but if you want to test Safari, IE or Cordova apps, then you should consider using webdriver.io.

### [Cypress](https://www.cypress.io/)

[Check out Cypress AE documentation](packages/e2e-cypress/README.md)

### [WebDriver.io](https://webdriver.io/) (wdio) **DEPRECATED**

> You're looking at Quasar v1 WebDriver.io AE docs. This AE has been deprecated and won't be migrated to support Quasar v2, you can find the announcement [here](https://github.com/quasarframework/quasar/discussions/10341)

```shell
quasar ext add @quasar/testing-e2e-wdio
yarn selenium:install && selenium:start
```

**WIP** - please help battle test this harness.
FYI: we're using webdriver 4.0 for the moment because wdio requires it. If you need to use webdriver 5, please get in touch and we can create another app-extension.

Prior Work:
[https://github.com/fansanelli/quasar-webdriver/blob](https://github.com/fansanelli/quasar-webdriver/)blob
[https://github.com/NodeJunkie/quasar-webdriver/tree/feat/BackportToQuasar%231](https://github.com/NodeJunkie/quasar-webdriver/tree/feat/BackportToQuasar%231)

### Quality Auditing

```shell
quasar ext add @quasar/testing-quality
```

Auditing the quality of your app is something you want to do before you go in production. Depending on your perspective, quality can mean many things. So we have put together a few tools that we think can help you have a qualitatively better project.

The `Lighthouse` tool can help you identify issues with your PWA app, but only if you serve the built version of your project. If you use it a lot, consider installing it globally.

`Snyk` is a tool for identifying node modules that have security implications. Running this regularly will keep you alerted to issues that may be stemming from repositories you use.

`Node License Finder (nlf)` is a free tool you can use to catalog all the licenses of the hundreds of open-source projects you are using in your project.
