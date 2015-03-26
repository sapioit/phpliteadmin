# Running phpLiteAdmin with PHP only #

phpLiteAdmin is written in PHP, and so it needs a php parser to run. And as it is a web application it also needs a webserver. But this doesn't mean you need to install and configure a full-blown webserver like Apache on your system. All you need to do is download php, unzip it, run the built-in server and open phpLiteAdmin in the browser. That's possible because php 5.4 includes a tiny webserver that offers all you need.

**No administrator/root rights required**. No installation, no registry changes. Simple cleanup by deleting the folder.

This works on any system that PHP supports. I will explain it with examples from a windows system, but it works more or less the same on other operating systems.


# How it's done #

  * [Download phpLiteAdmin](https://code.google.com/p/phpliteadmin/downloads/list)
  * Unzip it. Let's say to C:\Users\username\Desktop\phpLiteAdmin
  * Download php (>=5.4). [PHP 5.5.8 for Windows](http://windows.php.net/downloads/releases/php-5.5.8-nts-Win32-VC11-x86.zip), [other versions](http://php.net/downloads.php)
  * Unzip it. Let's say to C:\Users\username\Desktop\phpLiteAdmin\php
  * Start the built-in webserver: Type [Windows](Windows.md)+[R](R.md), type "cmd" and hit enter to get a black command-window. Then type:
```
cd c:\Users\username\Desktop\phpLiteAdmin
php\php.exe -S localhost:8000
```
  * Drop your databases you want to manage in C:\Users\username\Desktop\phpLiteAdmin
  * Now open your browser (leave the command-window open) and open this address: [http://localhost:8000/phpliteadmin.php](http://localhost:8000/phpliteadmin.php). The default password is "admin".
  * When you are done, close the command window to stop the built-in webserver
  * You can move your dbs out of the folder and delete it to clean up everything

If you think this is useful, drop a comment so we know if it's worth to offer a bundled version that makes things even easier.