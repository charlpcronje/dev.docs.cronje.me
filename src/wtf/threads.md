---
title: WTF Moments, Safe and unsafe threads | CRONje.ME
label: Thread safety. Safe and unsafe threads
order: 20
authors:
  - name: Charl Cronje
    email: charl@cronje.me
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

## What is thread safety

> A function is said to be thread-safe if and only if it will always produce correct results when called repeatedly from multiple concurrent threads.

If your functions are not thread-safe then it is likely that they will cause some WTF moments? Also the frequency of such moments will increase incrementally is the requests to the function increases

### How to make a function or code block thread safe in C#

You can use the `lock` keyword to make sure only one thread has access to the block of code at any one time:

```C#
var counter = 0;
var padLock = new object();

void count(int valueToAdd) {
    lock(padLock) {
        // Thread safe
        counter += valueToAdd;
    }
}
```

- **Important:** You can not use the `lock` keyword with `async` `await`, so that makes it sort of useless in many ways since async code has become so wide spread. 
- But you can use a `SemaphoreSlim()` class to achieve the same

```C#
var counter = 0;
// Put `1` as the argument stating that only one thread can now access class while it is being waited on
var semaphore = new SemaphoreSlim(1);
await count(5);

async Task count(int valueToAdd) {
    // Await 
    await semaphore.WaitAsync();
    try {
        await ComputeAsync(valueToAdd);
    // You should release your semaphore in a finally block so that you know it will always run so that you don't create a dead lock
    } finally  {
        semaphore.Release();
    }
}
```

### When is SQL thread safe and what makes it safe

- `MySQL` uses `locks` for `Isolation`, and `transactions` for `Atomicity`. Transactions require `InnoDB` or `BDB`. `InnoDB` supports full `ACID` support.
- By default, `MySQL` has `implicit transactions`.
- `MyISAM` uses table locking, whereas `InnoDB` provides row level locking

### In some cases the same can be achieved without having to worry about it

#### Working with transactions

- When you want to create a thousand entries into a database, and you want unique ID's for each row, the typical way to do this would simply to to a thousand inserts with for instance MySQL and if you want to know what the ID's were, you can ask MySQL what the auto_increment_id is. This could be safe and unsafe and very safe.
- If you do your insert and query for the auto_increment_id in two different transactions, it could very well happen that another insert is done before you ask for the ID and therefor you might get the same ID for two rows, not because there are two rows with the same ID but the you asked for the same ID twice.
Another option is to ask MySQL what the next ID will be before you do the insert and instead of letting MySQL add the auto_increment_id for you, you specify the ID with the one you received. This will again work if you do the asking and the inserting within the same transaction. 
- Both the above examples will potentially work, but only if you work with a database that supports transactions.

#### Doing the same without transactions

- I think that as a norm we tend to let SQL come up with it's own ID's it just feels right and we suspect that joining on numbers should be faster because, well is is a number.
- But what is a number in binary and what is a character in binary or a string in binary.

You can set your table / tables to `utf8_bin` like this

Replace `<database-name>` with the name of the database

```SQL
SELECT DEFAULT_COLLATION_NAME FROM information_schema.SCHEMATA S WHERE schema_name = '<database-name>' AND DEFAULT_COLLATION_NAME != 'utf8_bin';

SELECT * FROM information_schema.COLUMNS WHERE table_schema = '<database-name>' AND collation_name != 'utf8_bin';

SELECT * FROM information_schema.TABLES WHERE table_schema = '<database-name>' AND table_collation != 'utf8_bin';
```

Run the following to make it a database default


```SQL
ALTER DATABASE <database-name> CHARACTER SET utf8 COLLATE utf8_bin;
```

Alter the collation of a table with the below query;

```SQL
ALTER TABLE <table-name> CONVERT TO CHARACTER SET utf8 COLLATE utf8_bin;
```

Now that we know that we can update out tables to binary, and we know that indexes don't need to be a number to behave and index like one, we can do something else.

Now you can create a thousand entries but we don't let SQL decide what the `ID's` will be at all, we rather use a random `uuid()` function to generate ID's for us. This way you can have a thousand thread running at the same to insert a thousand rows and you'd know what each ID is without transactions and without asking for any `ID's`.

So if the id does not need to be a number and you are not using it for some kind of partitioning then rather use `uuid's` for id's, there are some security implications for using `uuid's` (better for security) and there are some other downsides. But in most cases when you are worried about `thread-safety` when working with SQL inserts etc, try using `uuid's`

## Is PHP thread-safe, doesn't PHP run ona single thread?

Yes, it correct that PHP does run on a single thread, but Apache does not. There is also a way to run PHP in multiple thread and to compile the executable to be thread-safe and or not to be. The difference really lies with what you are trying to achieve. Thread-safety switched off, makes your code run a bit faster, so if you know what you are doing regarding your threads and you want more speed, you could potentially get about a 20% increase in some cases but in others you might not even notice any change.

I am sure tha most developers are aware of how files can be blocked by one process when you use something like `file_get_contents`. It is easy to understand that you can't write different things to the same file on two different threads and expect it to just merge the changes and just work by magic. Certain things about thread safety easily makes sense but other's not so much.

### Some thread-unsafe functions in PHP

`shmop_read` and `shmop_write`

The two `functions` I mentioned above are used to `read` and `write` shared memory between `requests`, and in this care you would need to use a `semaphore` to make it `thread-safe`

```php
shmget(0x74613e35,0x64,0x3a4,0x3,0x1,0x7fffffffb9c8) = 65540 (0x10004)
shmctl(0x10004,0x2,0x7fffffffb960,0x3,0x1,0x7fffffffb9c8) = 0 (0x0)
shmat(0x10004,0x0,0x0,0x3,0x1,0x7fffffffb9c8) = 34369576960 (0x800962000)
^CSIGNAL 2 (SIGINT)
process exit, rval = 0
```

## Conclusion

`WTF moments` because if `thread-safety` issues can happen, and I think just to be aware of `thread-safety` will at least make you think about something like this when you have a `WTF moment`. It is not realistic to go and find out which `functions` in which languages are safe and which are not. Usually when you Google a `function` of a specific language and it is not a `thread-safe` `function`, it will be mentioned somewhere, where it is visible enough so that it will be noted by developers




