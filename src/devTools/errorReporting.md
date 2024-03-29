---
title: Dev Tools - Error Reporting
label: Error Reporting
order: 143
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
tags: [dev,tools,start,js,php,frontend,backend,developer,devtools,error,reports]
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

# Dev Tools - Error Reporting

Usually the error_reporting is disabled in `php.ini`.

The Dev Tools switches it back on by:

```php
ini_set('error_reporting','E_WARNING');
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_WARNING);
```

Notices are still switched off, this is just to save some time and they are 99% of the time  nothing to worry about, it is good practice to even fix your notices but most of out systems are full of notices and will take a long time to fix

The Dev Tools also calls the `set_error_handler` directive to set up a custom error handler. This is so that the consoleLog devTool can function. Otherwize PHP stops with the code execution before it can output the necessary Javascript to log to the console.

```php
set_error_handler(?callable $callback, int $error_levels = E_ALL): string|array|object|null
```
