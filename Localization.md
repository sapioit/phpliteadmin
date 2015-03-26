# About Localization #

Starting with version 1.9.4, phpLiteAdmin can be translated into different languages. By default, it comes with the English localization. More localizations can be downloaded from our web site (see below).
It is also easy to translate phpLiteAdmin in your own language if no translation is available yet.

# Download a Localization #
  * [Arabic localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_ar_1-9-4.zip)
  * [Chinese localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_cn_1-9-4.zip)
  * [Czech localization for 1.9.5](https://bitbucket.org/phpliteadmin/public/downloads/phpliteadmin_lang_cz-1.9.5.zip)
  * [French localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_fr_1-9-4_correction1.zip)
  * [German localization for 1.9.5](https://bitbucket.org/phpliteadmin/public/downloads/phpliteadmin_lang_de_1-9-5.zip)
  * [Greek localization for 1.9.5](https://bitbucket.org/phpliteadmin/public/downloads/phpliteAdmin_lang_gr_1-9-5.zip)
  * [Italian localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_it_1-9-4.zip)
  * [(Brazilian) Portuguese localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_pt_1-9-4.zip)
  * [Russian localization for 1.9.4](http://code.google.com/p/phpliteadmin/downloads/detail?name=phpliteAdmin_lang_ru_1-9-4_correction1.zip)
  * [(Latin-American) Spanish localization for 1.9.5](https://bitbucket.org/phpliteadmin/public/downloads/phpliteAdmin_lang_esla_1-9-5.zip)


**Note:** You can use old localization files for newer versions, but some added texts will still be English. See chapter "changes in localization files" below.

Localization-files should be called lang\_xx.php with xx being the language code for the corresponding language as defined by [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes), e.g. "de" for German.

# Install a Localization #

To install a localization, download the corresponding file and drop it into one of the following two places:
  * the folder in which you installed phpLiteAdmin (where the phpliteadmin.php file is)
  * the subfolder "languages"

To use the language, you need to configure it. So in your configuration, set `$language = "xx";` with xx being the language code of your language (e.g. "en" or "de"). See [Configuration](Configuration.md) for details.

# Translate phpLiteAdmin into your language #

You can easily translate phpLiteAdmin into your language. If you do so, please don't forget to send us your localization so we can make it available to other users!

To create your own localization:
  1. Search for the language code of your language in [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). _Example_: `de` for German
  1. Download the [English localization lang\_en.php](https://bitbucket.org/phpliteadmin/public/downloads/phpliteAdmin_lang_en_1-9-5.zip)
  1. Rename it to "lang\_xx.php" with xx being the language code. _Example_: `lang_de.php`
  1. Open the file in a texteditor. Translate the texts (see below) and save the file.
  1. Install the localization to test it (see above).
  1. Please [[us your localization](https://groups.google.com/forum/#!forum/phpliteadmin|send)] so we can make it available to other users. This is a community project, we need your contribution!

## How to do the actual translation ##
Language files are normal php-files that define an array called `$lang`. Therefore, they start like this:
```
<?php
$lang = array(
```
And end like this:
```
);
?>
```
If you want to, you can add a comment at the beginning of the file with your name like this:
```
<?php
// German translation by Christopher Kramer
$lang = array(
```
The rest of the file is the actual translation. It looks like this:
```
	"direction" => "LTR",
	"date_format" => 'g:ia \o\n F j, Y (T)',
	"ver" => "version",
	"for" => "for",

```
At the left side before `=>`, there is the key of the language-text. In the code above, the keys are "direction", "date\_format", "ver" and "for". **Never translate or change the key.** On the right side after `=>`, the value follows in the language of the translation. For example for the key "ver", the value "version" is defined. You can now translate the value into your language. For example the Spanish word for "version" is "versión". So the translated file would look like this:
```
	"direction" => "LTR",
	"date_format" => 'g:ia \o\n F j, Y (T)',
	"ver" => "versión",
	"for" => "for",

```

To do the translation, you go through the file line by line and translate the values into your language.
There are some special keys with special values like "direction" or "date\_format" that are not that obvious how to translate them. You will find an explanation for these below.

You don't have to translate everything if you don't want to. You could for example leave some error messages and the help documentation in English and only translate the important texts.

For those of you who do not know PHP some additional remarks:
  * Make sure each value is enclosed by either double quotes or single quotes and after the quotes, **there is a comma at the end of the line**
  * If you want to use quotes in the value and the value is enclosed in the same type of quotes (i.e. also single quotes or also double quotes), you must escape them by putting a backslash before the quote. _Example_: `"key" => "some \"test in double quotes\"",`
  * If you use double quotes and want to use a dollar sign in your value, you should escape it using a backslash. _Example_: `"key" => "US currency: \$",`
  * Everything after `//` or `#` is only a comment. This is some advice for you, no need to translate it. Comments can also start with `/*` and end with `*/` (multi-line comments).

### Special translation keys and their values ###
**direction** : direction the texts are written. Possible values:
  * **LTR** = left to right (used for most languages like English, German, Spanish, French, ...)
  * **RTL** = right to left (used for Arabic languages for example)
**date\_format** : Format in which dates are printed. Special characters stand for the day, month, year, hour and so on. For example "d" stands for "Day of the month, 2 digits with leading zeros". You can find the list and definition of these special characters in the [documentation of the PHP date function](http://php.net/manual/en/function.date.php). If you want to put text in here that should not be replaced, escape it using a backslash._Example_: `g:ia \o\n F j, Y (T)`. Here the text "on" is put between the time and the date. (Note: use single quotes for simplicity here. If you use double quotes, you might need to double-escape things because `\n` would stand for a line-break.)

If there is some other key you don't understand, please ask in the comments.

## Ask in case of problems ##
In case you have problems translating phpLiteAdmin, we will try to help you. Just ask in the comments.
It might be the case that something is not possible to translate into some language because we made things not flexible enough. If you think this is the case, then please let us know and we will adjust things in the next version.

## Changes in localization files ##
With new versions, we usually need to add new language texts. This means localization files need to be updated. You can use old localization files with new version, but the texts that were added in the new version will then be in English.
If you are a translator, here is the list of changes that we did with the lasts versions so you know what you need to add:

| **key** | **English value** | **Added in** | **comment**  |
|:--------|:------------------|:-------------|:-------------|
| no | No | 1.9.5 |  |
| none | None | 1.9.5 |  |
| as\_defined | As defined | 1.9.5 |  |
| expression | Expression | 1.9.5 |  |
| as\_defined | As defined | 1.9.5 |  |
| ques\_primarykey\_add | Are you sure you want to add a primary key for the column(s) %s in table '%s'? | 1.9.5 |  |
| ques\_column\_delete | Are you sure you want to delete column(s) %s from table '%s'? | 1.9.5 | only the key was renamed, before it was ques\_del\_col |

Please send updated language files to our [discussion group](https://groups.google.com/forum/#!forum/phpliteadmin).