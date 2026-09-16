# Mukurtu CMS v4 Project Template

This template only covers getting a Mukurtu site's code and database in place. For the full Mukurtu repository and information, see [Mukurtu CMS]([url](https://github.com/MukurtuCMS/Mukurtu-CMS)).

## Requirements
* The necessary database server, web server, and PHP installed that meet [modern Drupal requirements](https://www.drupal.org/docs/system-requirements)
  * PHP 8.4 is supported.
  * Currently MariaDB or MySQL is supported. PostGRES is not.
  * The Mukurtu Team does our internal work with nginx. Apache SHOULD work fine, but we have not tested it extensively.
* [Composer](https://getcomposer.org/)
* To generate PDF thumbnails, [poppler-utils](https://pypi.org/project/poppler-utils/) must be installed on the server.
* To generate thumbnails for uploaded video files, [FFmpeg](https://ffmpeg.org/) must be installed on the server.
* For local development, we encourage using [Docker](https://ddev.readthedocs.io/en/stable/users/install/docker-installation/) and [DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/) (which includes composer)

## Install Mukurtu with DDEV

Using DDEV is the easiest way to get up and running with Mukurtu locally.

* Download and install [DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/)
* Make a new folder in which to work and initialize a DDEV project inside it. Run the following commands to download and install Mukurtu.
```
mkdir mukurtu
cd mukurtu
ddev config --project-type=drupal --docroot=web
ddev start
ddev composer create-project mukurtu/mukurtu-template:^4.0
ddev drush si --site-name=Mukurtu --account-name=admin --account-pass=admin
ddev launch
```

**Note:** This template includes `drupal/devel` and `drupal/devel_php` in
`require-dev`, so they install by default unless you pass `--no-dev` to
`composer create-project`. Mukurtu no longer enables Devel automatically, so both
packages sit inert on disk until you turn them on. `devel_php` specifically provides
an execute-PHP capability, so enable it deliberately.

* If planning to develop on the Mukurtu CMS installation profile, follow the [additional installation steps to connect a Git checkout to the new project](https://github.com/MukurtuCMS/Mukurtu-CMS/wiki).

## Installing Mukurtu CMS with Composer

If installing directly on a web host that has a command line interface, you can install Mukurtu via composer.

**Database requirement:** Create your database using the `utf8mb4` character set and `utf8mb4_general_ci` collation. Using plain `utf8` can cause issues with content that includes characters outside the Basic Multilingual Plane (e.g. emoji). This follows [Drupal's recommendation](https://www.drupal.org/docs/getting-started/system-requirements/database-server-requirements) for MySQL/MariaDB:

```sql
CREATE DATABASE mukurtu CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

* First, [install composer](https://getcomposer.org/download/). If you do not have it already, it can be downloaded into a directory with the following:
```
wget https://raw.githubusercontent.com/composer/getcomposer.org/main/web/installer -O - -q | php -- --quiet
# Ideally, move composer into an executable path such as /usr/local/bin/composer.
# But for use only within the current directory, just rename it.
mv composer.phar composer
```
* Install Mukurtu through composer with the following commands:
```
mkdir mukurtu
cd mukurtu
composer create-project mukurtu/mukurtu-template:^4.0 .
```

**Note:** This template includes `drupal/devel` and `drupal/devel_php` in
`require-dev`, so they install by default unless you pass `--no-dev` to
`composer create-project`. Mukurtu no longer enables Devel automatically, so both
packages sit inert on disk until you turn them on. `devel_php` specifically provides
an execute-PHP capability, so enable it deliberately.

* Set your web server to serve the "web" folder (e.g. `mukurtu4/web`)
* Install Drupal as normal by opening the site in your web browser, the Mukurtu profile distribution will automatically be used.

## After Installing

This template only covers getting a Mukurtu site's code and database in place. For
post-installation setup (private files, `pdftotext`), updating an existing site, and
troubleshooting, see the [Mukurtu CMS README](https://github.com/MukurtuCMS/Mukurtu-CMS#post-installation-steps).
