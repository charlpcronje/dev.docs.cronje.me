# ISA Dev Tools - Getting Started

> In an ideal word the dev tools would be loaded from a remote server so that I don't have to keep on deplaying the dev tools on every server. After some playing around for a while I created a Docker container serving each script on a different por. For now I'm still playing around with some more ideas._

```shell
    nano /etc/httpd/conf/httpd.conf
```

Where is says `AllowOverride none`, change that so that it says `AllowOverride All`, save (CTRL O) and exit (CTRL X)
Copy .htaccess file that is located in the `tools/system` folder to the root of the project you are editing. Now all traffic will be routed to `/tool/system/prepend.php`
This will add the dev-tools to the execution of the code, them the prepend script will include the file that was supposed to opened in the first place.

```php
    include('https://192.168.9.101/init.php');
```

The following needs to be set to 'On' in the `php.ini` file.

```conf
`allow_url_include = On`
```

If you do not have access to the php.ini you can simply upload the tools folder to the public_html folder, then the following to the file.

```php
    include('include('tools/init.php');
```

Thats it, just include and use
