# Internal vs External Configuration #

Until version 1.9.4, phpLiteAdmin could only be configured editing the phpLiteAdmin.php file. Starting from 1.9.4, we now search in the current directory for an external configuration file named ''phpliteadmin.config.php''. If this file is found, it will be `include`d and will override the internal default value.

You can now choose between two configuration options:

  * edit the code of of the main phpliteadmin.php
    * settings are easy to find at the top of the file
    * you can deploy phpLiteAdmin by copying a single, self-contained file on your server
    * when you update phpLiteAdmin, you will need to manually copy your settings to the new version
  * create an external configuration file named ''phpliteadmin.config.php'' (or just rename the sample supplied)
    * your configuration will be self-contained
    * you will need to copy more two files to deploy phpLiteAdmin
    * updating phpLiteAdmin is easier because you don't need to edit the main file, but check the release notes or the new sample configuration for new options!

The configuration in both files follows the same format, and must be valid PHP code. Please note the use of quotes or double quotes, and don't forget your semi-colons!

Below a short descriptions of the options available starting from 1.9.4.


## Main configuration ##

  * `$password` is the text you need to enter to gain access to phpLiteAdmin; the default password is 'admin', remember to change it!
  * `$directory` will tell phpLiteAdmin where to look for sqlite files; found databases will appear in the database list;
  * `$subdirectories` should be set to `true` if you want phpLiteAdmin to search all subdirectories of `$directory`; otherwise, search will be limited to the specified path;
  * `$databases` can be used to list specific databases that you want to manage through phpLiteAdmin; is `$directory` (above) is set to `false`, these will be the only files available.


## Interface settings ##

  * `$theme` is a css file which defines how phpLiteAdmin looks like in your browser, see the [Themes](Themes.md) list;
  * `$language` allows [Localization](Localization.md) of the phpLiteAdmin interface; as of 1.9.4, only English (`en`) and German (`de`) are available;
  * `$rowsNum` decides how many rows will be shown in each page when browsing a table;
  * `$charsNum` specifies the maximum length of strings appearing in table rows; anything longer will be cut with ellipsis (`...`).


## Custom functions ##

  * `$custom_functions` is an array listing all user-defined function which can be applied to values through phpLiteAdmin;
  * Your custom functions should be defined _somewhere_: you can include another php file, or define them in this section of the main/external configuration.


## Advanced options ##

  * `$cookie_name` can be used to run multiple instances of phpLiteAdmin on the same domain: just choose a unique string for each instance;
  * `$debug` is a boolean flag that enables additional debug output;
  * `$allowed_extensions` lists the php extensions that phpLiteAdmin will consider when opening or creating a database.
