---
title: Material Design Icons - CRONje.ME
label: Material Design Icons
order: 1
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

Material Design Icons' growing icon collection allows designers and developers targeting various platforms to download icons in the format, color and size they need for any project.

> Material Design Icons has been around for many years and is compatible with many technologies and frameworks. Please view the docs menu at the top for an appropriate getting started guide.

## Using the Webfont

One of the easiest ways to use the icons is through the webfont. There is also a hosted CDN option for quick use in demos or development.

[Learn More (Webfont - Getting Started)](https://dev.materialdesignicons.com/getting-started/webfont)

> Using the webfont while easy to use is highly discouraged due to performance and overall request size. Please read the Webfont Alternatives Guide for more details.

## Using SVGs

All icons are designed in vector and provided in SVG format.

## As an Image File3

SVGs can be downloaded individually and included the same way as any bitmap image:

```html
<img src="/path/to/icons/example-icon.svg" alt="An example icon" style="width:24px;height:24px" />
```

## Inline SVG

SVG's can be used inline in the HTML.

```html
<svg style="width:24px;height:24px" viewbox="0 0 24 24">
  <path fill="#000000" d="M ... Z" /> <!-- account -->
</svg>
```

Inline `SVGs` can also be `overlayed` by adding additional paths.

```html
<svg style="width:24px;height:24px" viewbox="0 0 24 24">
  <path fill="#000000" d="M ... Z" /> <!-- account -->
  <path fill="#990000" d="M ... Z" /> <!-- block-helper -->
</svg>
```