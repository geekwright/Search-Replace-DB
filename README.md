# srdb - Search Replace DB for XOOPS

This is a XOOPS adaptation of [Search and Replace DB](https://github.com/interconnectit/Search-Replace-DB) from interconnect/it.

You can use **srdb** to make database changes when you move a XOOPS installation
to a different server or domain, including moving a site to **SSL/https**.

## Quick Start Guide
 - **Make a backup of your database!**
 - Download and unzip the [srdb archive](https://github.com/geekwright/srdb/archive/xoops.zip)
 - copy the folder to the root of your site
 - open the folder you just uploaded in your browser, i.e. https://example.com/srdb/
 - enter the string associated with your OLD site in the *replace* field, i.e. http://localhost
 - enter the equivalent string for your NEW new site in the *with* field, i.e. https://example.com
 - in the *Actions* section choose *dry run* to review what will be changed
 - if everything looks correct, choose *live run* to replace the strings in the database
 - repeat as needed for other strings, such as OLD and NEW server file paths
 - remove the srdb folder from your site (Leaving it is a **security risk!**)

## Going Further
You can be much more precise by choosing certain tables and certain columns to work with.

There are also many other options available, such as converting the MySQL engine used by tables,
updating the character sets, and more.

It is also possible to create scripts to run from the command line, allowing you to build
and test a conversion to run at a later time. This way you can automate the actual cut-over
process to minimize downtime during a site move.

For more information read through the full *interconnect/it* README below.

**The following is the original README from interconnect/it**
# Search Replace DB

This script was made to aid the process of migrating PHP and MySQL based websites. It has additional features for WordPress and Drupal but works for most other similar CMSes.

If you find a problem let us know in the issues area and if you can improve the code then please fork the repository and send us a pull request :)

## Warnings & Limitations

1. Three character UTF8 seems to break in certain cases.
2. We can't test every possible case, though we do our best. Backups and verifications are important.
3. The license for this script is GPL v3 and no longer WTFPL. Please bear this in mind if contributing or branching.
4. You use this script at your own risk and we have no responsibility for any problems it may cause.
5. *Do backups.*

## Usage

1. *Do backups.*
2. Migrate all your website files.
3. Upload the script folder to your web root or higher.
4. Browse to the script folder URL in your web browser.
5. Fill in the fields as needed.
6. Choose the `Dry run` button to do a dry run without searching/replacing.

## Installation

If you would like Search Replace DB to detect your WordPress installation, you should install it within a new subfolder within your WordPress installation.

For example, if you have

	/website.com/index.php

	/website.com/wp-config.php

	/website.com/wordpress/

	/website.com/wordpress/index.php

	/website.com/wordpress/wp-settings.php

	etc.

You can copy Search Replace DB into the following location:

	/website.com/wordpress/Search-Replace-DB/

	/website.com/wordpress/Search-Replace-DB/index.php

	/website.com/wordpress/Search-Replace-DB/srdb.class.php

	/website.com/wordpress/Search-Replace-DB/srdb.cli.php

	etc.

### CLI script

To invoke the script, nagivate in your shell to the directory to where you installed Search Replace DB.

Type `php srdb.cli.php` to run the program. Type `php srdb.cli.php --help` for usage information:

	-h, --host

		Required. The hostname of the database server.

	-n, --name

		Required. Database name.

	-u, --user

		Required. Database user.

	-p, --pass

		Required. Database user's password.

	--port

		Optional. Port on database server to connect to.
		The default is 3306. (MySQL default port).

	-s, --search

		String to search for or `preg_replace()` style regular
		expression.

	-r, --replace

		None empty string to replace search with or
		`preg_replace()` style replacement.

	-t, --tables

		If set only runs the script on the specified table, comma
		separate for multiple values.

	-i, --include-cols

		If set only runs the script on the specified columns, comma
		separate for multiple values.

	-x, --exclude-cols

		If set excludes the specified columns, comma separate for
		multiple values.

	-g, --regex [no value]

		Treats value for -s or --search as a regular expression and
		-r or --replace as a regular expression replacement.

	-l, --pagesize

		How many rows to fetch at a time from a table.

	-z, --dry-run [no value]

		Prevents any updates happening so you can preview the number
		of changes to be made

	-e, --alter-engine

		Changes the database table to the specified database engine
		eg. InnoDB or MyISAM. If specified search/replace arguments
		are ignored. They will not be run simultaneously.

	-a, --alter-collation

		Changes the database table to the specified collation
		eg. utf8_unicode_ci. If specified search/replace arguments
		are ignored. They will not be run simultaneously.

	-v, --verbose [true|false]

		Defaults to true, can be set to false to run script silently.

	--help

		Displays this help message ;)

## Troubleshooting

### I get a popup saying there was an AJAX error

This happens occasionally and could be for a couple of reasons:

 * When the script starts, it attempts to start your WordPress or Drupal installation to auto-detect your username and password settings. If this fails, you will see a message informing you that auto-detection failed. You will have to enter your details manually.
 * Script was unable to set the timeout so PHP closed the connection before the table could be processed, this can happen on some server configurations.
 * When using php-fpm (as you have with VVV) make sure that the socket is owned by the server user `chown www-data:www-data /var/run/php5-fpm.sock`.
