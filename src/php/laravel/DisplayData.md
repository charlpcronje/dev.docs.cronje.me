---: Displaying Data | DEVserv.ME
label: Displaying Data
order: 12
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
tags: [dev,tools,js,frontend,backend,devtools,php,laravel]
---
# Displaying Data

Now that we have made the `users` available to our view, we can display them like so:

```php
    @extends('layout')

    @section('content')
        @foreach($users as $user)
            <p>{{ $user->name }}</p>
        @endforeach
    @stop
```

You may be wondering where to find our `echo` statements. When using Blade, you may echo data by surrounding it with double curly braces. It's a cinch. Now, you should be able to hit the `/users` route and see the names of your users displayed in the response.
