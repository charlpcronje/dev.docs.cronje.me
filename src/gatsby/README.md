---
title: Gatsby + Netlify CMS Starter | CRONje.ME
label: Gatsby + Netlify CMS Starter
order: 140
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,start,js,php,frontend,backend,developer,devtools,helpers,log]
---

**Note:** This starter uses [Gatsby v2](https://www.gatsbyjs.org/blog/2018-09-17-gatsby-v2/).

[Download the example apps](gatsby/gatsby-starter-netlify-cms-master.zip)

## Features



Please read the message above, I also recorded it so you can just play and listen. This should be my last message for now, I saw the messages was a bit messy because of the two chats apps. I'd really appreciate it if you once again did me this favor to read what I've sent you above and to at least open the links and check it out and maybe bookmark them for later of you don't feel like looking at it immediately or if you want to go back later to continue.
Please don't spite me in this or make me wonder about things for no reason. In the end you're getting what you wanted (me off your case) but for more than two years I've never been allowed one thing to give me any closure, or one explanation of what is actually going on or why you are blaming me instead of the people who deserve it and why after we were best friends and I proved my loyalty to you over, why then after we started dating a fell in love did you decide to push me away and accuse me of so many messed up things when I've been the only person not using you or taking advantage of you and your situation. It been very hard to deal with the fact that you'd rather be with drunk strangers of any race, or creed and not caring where and in what way and if his friends wants to watch or join or cheer or shout and make remarks, than to accept any of the opportunities I've presented you that will make you more money and a safe place.
So I've come to understand I lot of things and I don't blame you or hate you or think any less of you. I do blame the people who deserve it, I do blame the people who made that the only thing you know and who has now convinced you that you are fine there even though you never wanted to be back in that life and you could be making more for giving less and have a real life and you could be following your dreams again.
I'm not refusing to give you money for gambling because I'm an asshole or because I can't afford it, you can ask Jaime, I've been helping her out when she's been in trouble. But I don't see why you have to be there at all, why you should bot gave an ID card and your own bank account earing more money and being able to gamble all day and night. I don't have to be tortured any more, you know how to reach me and I know you actually know you can trust me. You don't have to pretend with me and you don't have to use me. You can have everything you want and will ever need by simply taking what I offer you and then being able to look after yourself making more than a million rand a year and dating who you want and doing what you want.
So please stop making me out for something I'm not and stop lying to yourself and stop acting like it does not matter what you do or who takes advantage of you. Because it does matter, you absolutely do matter, your wellbeing matters and you being in a place where you can really be happy and being all you can be is something that use to matter to you a great deal. 
Please read the message above, please then think about what you are giving up and for what reason and make a decision that will really be the best for you and what you can be proud of when you look back one day.
I hope to year from you soon or at least some day.
With all my love and hope.
Charl


- A simple landing page with blog functionality built with Netlify CMS
- Editable Pages: Landing, About, Product, Blog-Collection and Contact page with Netlify Form support
- Create Blog posts from Netlify CMS
- Tags: Separate page for posts under each tag
- Basic directory organization
- Uses Bulma for styling, but size is reduced by `purge-css-plugin`
- Blazing fast loading times thanks to pre-rendered HTML and automatic chunk loading of JS files
- Uses `gatsby-image` with Netlify-CMS preview support
- Separate components for everything
- Netlify deploy configuration
- Netlify function support, see `lambda` folder
- Perfect score on Lighthouse for SEO, Accessibility and Performance (wip:PWA)
- ..and more

## Prerequisites

- Node (I recommend using v8.2.0 or higher)
- [Gatsby CLI](https://www.gatsbyjs.org/docs/)
- [Netlify CLI](https://github.com/netlify/cli)

## Getting Started (Recommended)

Netlify CMS can run in any frontend web environment, but the quickest way to try it out is by running it on a pre-configured starter site with Netlify. The example here is the Kaldi coffee company template (adapted from [One Click Hugo CMS](https://github.com/netlify-templates/one-click-hugo-cms)). Use the button below to build and deploy your own copy of the repository:

After clicking that button, you'll authenticate with GitHub and choose a repository name. Netlify will then automatically create a repository in your GitHub account with a copy of the files from the template. Next, it will build and deploy the new site on Netlify, bringing you to the site dashboard when the build is complete. Next, you'll need to set up Netlify's Identity service to authorize users to log in to the CMS.

### Access Locally

Pulldown a local copy of the Github repository Netlify created for you, with the name you specified in the previous step
```
$ git clone https://github.com/[GITHUB_USERNAME]/[REPO_NAME].git
$ cd [REPO_NAME]
$ yarn
$ netlify dev # or ntl dev
```

This uses the new [Netlify Dev](https://www.netlify.com/products/dev/?utm_source=blog&utm_medium=netlifycms&utm_campaign=devex) CLI feature to serve any functions you have in the `lambda` folder.

To test the CMS locally, you'll need to run a production build of the site:

```
$ npm run build
$ netlify dev # or ntl dev
```

### Media Libraries (installed, but optional)

Media Libraries have been included in this starter as a default. If you are not planning to use `Uploadcare` or `Cloudinary` in your project, you **can** remove them from module import and registration in `src/cms/cms.js`. Here is an example of the lines to comment or remove them your project.

```javascript
import CMS from 'netlify-cms-app'
// import uploadcare from 'netlify-cms-media-library-uploadcare'
// import cloudinary from 'netlify-cms-media-library-cloudinary'

import AboutPagePreview from './preview-templates/AboutPagePreview'
import BlogPostPreview from './preview-templates/BlogPostPreview'
import ProductPagePreview from './preview-templates/ProductPagePreview'
import IndexPagePreview from './preview-templates/IndexPagePreview'

// CMS.registerMediaLibrary(uploadcare);
// CMS.registerMediaLibrary(cloudinary);

CMS.registerPreviewTemplate('index', IndexPagePreview)
CMS.registerPreviewTemplate('about', AboutPagePreview)
CMS.registerPreviewTemplate('products', ProductPagePreview)
CMS.registerPreviewTemplate('blog', BlogPostPreview)
```

Note: Don't forget to also remove them from `package.json` and `yarn.lock` / `package-lock.json` using `yarn` or `npm`. During the build netlify-cms-app will bundle the media libraries as well, having them removed will save you build time.
Example:
```
yarn remove netlify-cms-media-library-uploadcare
```
OR
```
yarn remove netlify-cms-media-library-cloudinary
```
## Getting Started (Without Netlify)

```
$ gatsby new [SITE_DIRECTORY_NAME] https://github.com/netlify-templates/gatsby-starter-netlify-cms/
$ cd [SITE_DIRECTORY_NAME]
$ npm run build
$ npm run serve
```

### Setting up the CMS

Follow the [Netlify CMS Quick Start Guide](https://www.netlifycms.org/docs/quick-start/#authentication) to set up authentication, and hosting.

## Debugging

Windows users might encounter `node-gyp` errors when trying to npm install.
To resolve, make sure that you have both Python 2.7 and the Visual C++ build environment installed.

```
npm config set python python2.7
npm install --global --production windows-build-tools
```

[Full details here](https://www.npmjs.com/package/node-gyp 'NPM node-gyp page')

MacOS users might also encounter some errors, for more info check [node-gyp](https://github.com/nodejs/node-gyp). We recommend using the latest stable node version.

## Purgecss

This plugin uses [gatsby-plugin-purgecss](https://www.gatsbyjs.org/packages/gatsby-plugin-purgecss/) and [bulma](https://bulma.io/). The bulma builds are usually ~170K but reduced 90% by purgecss.