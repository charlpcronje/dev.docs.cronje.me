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

> Material Design 

## Using the Webfont

One of the easiest ways to use the 

[Learn More (Webfont - Getting Started)](https://dev.materialdesign

> Using the webfont while easy to use is highly discouraged due to performance and overall request size. Please read the Webfont Alternatives Guide for more details.
          
## Using SVGs

All 

## As an Image File3

SVGs can be downloaded individually and included the same way as any bitmap image:

```html
<img src="/path/to/
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
