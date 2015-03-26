# Installation Instructions #

  1. <a href='https://code.google.com/p/phpliteadmin/wiki/DownloadLinks?tm=2'>Download</a> the latest version of phpLiteAdmin.
  1. Unzip and open the downloaded file, phpliteadmin.php, in a text editor.
  1. If you want to have a directory scanned for your databases instead of listing them manually, specify the directory as the value of the `$directory` variable. Also, you may choose to have all of its subdirectories scanned infinitely deep by setting the `$subdirectories` variable to true.
  1. If you want to specify your databases manually, set the value of the `$directory` variable as false and modify the `$databases` array to hold the databases you would like to manage.
    * The `path` field is the file path of the database relative to where phpliteadmin.php will be located on the server. For example, if phpliteadmin.php is located at `databases/manager/phpliteadmin.php` and you want to manage `databases/yourdatabase.sqlite`, the `path` value would be "../yourdatabase.sqlite".
    * The `name` field is the human-friendly way of referencing the database within the application. It can be anything you want.
  1. Modify the `$password` variable to be the password used for gaining access to the phpLiteAdmin tool.
  1. If you want to have multiple installations of phpLiteAdmin on the same server, change the `$cookie_name` variable to be unique for each installation _(optional)_.
  1. Save and upload phpliteadmin.php to your web server.
  1. Open a web browser and navigate to the uploaded phpliteadmin.php file. You will be prompted to enter a password. Use the same password you set in step 4.
  1. You may optionally edit the CSS or use one of the pre-made themes to customize the look of phpLiteAdmin. Follow the instructions described on the [Themes](Themes.md) page.

See [Configuration](Configuration.md) for the documentation of all configuration options.

## Dependency: SQLite library for PHP ##

_If you do not have a webserver and php installed yet and only want to run phpLiteAdmin, read the NoWebserver wikipage._

You need some SQLite library for PHP installed. This can be either:
  * PDO (with the SQLite driver installed)
  * SQLite3
  * SQLiteDatabase (version 2)

Usually PHP 5.3 upwards comes with one of these, but if phpLiteAdmin does not work, make sure one of them is installed.

On Ubuntu Linux, you might do so using:

`sudo apt-get install php5-sqlite`

On Debian:

`apt-get install php5-sqlite`

Of course you also need PHP >=5.1.0 installed and a webserver like apache.