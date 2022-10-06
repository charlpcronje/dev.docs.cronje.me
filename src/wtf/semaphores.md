---
title: WTF Moments, Semaphores | CRONje.ME
label: Thread safety. Semaphores
order: 20
authors:
  - name: Charl Cronje
    email: charl@cronje.me
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

A `semaphore` is a `variable` or `abstract` data type used to control access to a common resource by multiple threads and avoid critical section problems in a concurrent system such as a `multitasking` operating system. `Semaphores` are a type of `synchronization primitive`. A trivial `semaphore` is a plain `variable` that is changed (for example, `incremented` or `decremented`, or `toggled`) depending on programmer-defined conditions.

A useful way to think of a `semaphore` as used in a real-world system is as a record of how many units of a particular resource are available, coupled with operations to adjust that `record` `safely` (i.e., to avoid `race conditions`) as units are acquired or become free, and, if necessary, wait until a unit of the resource becomes available.

`Semaphores` are a useful tool in the prevention of `race conditions`; however, their use is by no means a guarantee that a program is free from these problems. `Semaphores` which allow an arbitrary resource count are called `counting semaphores`, while `semaphores` which are restricted to the values `0 and `1` (or `locked/unlocked`, `unavailable/available`) are called `binary semaphores` and are used to implement `locks`.

`Semaphores` are an important concept in thread safety, less in scripting languages like `PHP` but more in `Java`, `C#`

[Continue to WTF Moments](./README.md)
