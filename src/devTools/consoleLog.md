---
title: Console Log - Console Log
label: Console Log
order: 144
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,start,js,php,frontend,backend,developer,devtools,console,log]
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

The `ConsoleLog` or alias `CL` class is available to send logs to the browser console

```php
/**
 * All of the methods work the same, they are all static methods of the ConsoleLog class.
 * You can call them with or with or without the $value argument, when there is no $value specified then it is accepted that the $key is the value and it is added as the next item in the respective log array()
 * 
 * All of the methods will call the javascript `console.[method]` method with the same arguments accept for OBJ that will still call the `log` method but add {} around the argument which will make javascript handle the output json as a JS object
 * 
 * LOG: Log the value in Green and Bold
 * INFO: Log the value in Blue and Bold
 * WARN: Log the value in Orange and Bold
 * WARN: Log the value in Red and Bold
 * TABLE: This is for arrays, and it will output the array or multi-dimensional in table format with the array keys as column headings
 * OBJ: Will show the Object Key and It's contents as Key->value pairs next to it
 */

/**
 * Does console.log($key,$value) by calling a Javascript class called `Log` and method called `serverLog`
 */
ConsoleLog::LOG($key,$value = null);.
ConsoleLog::INFO($key,$value = null);
ConsoleLog::WARN($key,$value = null);
ConsoleLog::ERROR($key,$value = null);
ConsoleLog::TABLE($key,$value = null);
ConsoleLog::OBJ($key,$value = null);
```

OR

```php
/**
 * All of the methods work the same, they are all static methods of the CL class.
 * You can call them with or with or without the $value argument, when there is no $value specified then it is accepted that the $key is the value and it is added as the next item in the respective log array()
 */
CL::LOG($key,$value = null);.
CL::INFO($key,$value = null);
CL::WARN($key,$value = null);
CL::ERROR($key,$value = null);
CL::TABLE($key,$value = null);
CL::OBJ($key,$value = null);
```
