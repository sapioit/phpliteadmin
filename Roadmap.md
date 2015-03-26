# Roadmap #

The plan of the currently active team members is to incrementally improve and refactor phpliteAdmin.

Please see our [issue tracker](https://code.google.com/p/phpliteadmin/issues/list) for what is currently planned and request features there.

## phpLiteAdmin ~~v2.0~~ (complete rewrite) ##

**_UPDATE_ 2013-03-18: Currently, no active team member is planning to do a complete rewrite as described here. Instead, the active developers prefer to incrementally improve the current version of phpLiteAdmin step-by-step. This means adding new features like some of them mentioned below and improving maintainability and code structure. To get an idea of what we plan to do next, have a look at the [issue tracker](https://code.google.com/p/phpliteadmin/issues/list). You can also request new features there.**

~~phpLiteAdmin v2.0 will be a complete rewrite, starting from the ground up. We feel that by starting new we can make development for phpLiteAdmin much cleaner and more effective.~~

**_UPDATE_ 2013-03-25: As there is no plan (anymore) to do a complete rewrite, we plan to use the version number "2.0" as a normal version number. This means that what was called "phpLiteAdmin 2.0" here is not what we plan to release as 2.0. If there will ever be a complete rewrite, it will get a new name.**

There will be a difference in the way phpLiteAdmin is developed, as we will develop phpLiteAdmin ~~v2.0~~ from multiple source files. The reason for this is it will prevent any major conflicts when developers are making changes to phpLiteAdmin, as working on a single file can cause conflicts, which can result in major headaches. But don't worry! Whenever an official (or beta, RC, etc.) release becomes available, all source code files will be merged into a single file, just as it is now.
**UPDATE 2013-03-25: This is already done as of 1.9.5, see [issue #190](https://code.google.com/p/phpliteadmin/issues/detail?id=#190).**

These are the planned features ~~that will be available once phpLiteAdmin v2.0 reaches its final release~~:
  * Support for SQLite version 2 and 3.
  * Support for encrypted SQLite databases (version 3 only)
  * Creating, dropping, renaming, emptying, and modifying (adding, editing, and deleting columns) tables.
  * Browsing, adding, editing, and deleting rows.
  * A graphical interface for searching data.
  * Query builder.
  * Multiple user accounts.
  * The ability to specify which users can access which databases.
  * New theme system, allowing customization of the theme.
  * A robust importing and exporting feature, allowing the importation and exportation of large SQLite databases. Exporting will allow different formats such as CSV (per table), XML, HTML, and others to be determined.
  * Query exporter, which allows you to specify a SELECT query to export, allowing you to save the results of the query in a CSV, XML, HTML, and other formats.
  * The ability to quickly and easily update phpLiteAdmin, as when a new version is available you will be notified and asked to update. When you allow the update to occur, phpLiteAdmin will download the new version and set it up for you.

### Classes ###
Here is a list of all the classes ~~that will be involved in v2.0~~

**UserAuth**
Functionality to log in and log out user, check and authorize permissions, set cookies, etc.

**Database**
Generic database abstraction class to query, select, insert, and initialize the SQLite databases. Handles the distinguishing between different SQLite versions (2 vs. 3) and which PHP extension to use.

**DatabaseInfo**
Provides a way to get certain stats about the database like SQLite version, path, name, PHP extension, etc.

**DatabaseOperations**
Extended functions for the database like viewing, editing, creating, deleting, exporting, and importing rows and columns, exporting and importing tables and entire databases, performing custom queries, searching databases and tables, creating, editing, and deleting tables, etc.


---


**Current development status:** Suspended (there won't be a complete rewrite, see above)