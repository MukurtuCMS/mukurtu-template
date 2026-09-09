# Mukurtu CMS v4 Project Template

## Requirements
* The necessary database server, web server, and PHP installed that meet [modern Drupal requirements](https://www.drupal.org/docs/system-requirements)
* [Composer](https://getcomposer.org/)
* For local development, we encourage using [Docker](https://ddev.readthedocs.io/en/stable/users/install/docker-installation/) and [DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/) (which includes composer)

## Install Mukurtu with DDEV

Using DDEV is the easiest way to get up and running with Mukurtu locally.

* Download and install [DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/)
* Make a new folder in which to work and initialize a DDEV project inside it. Run the following commands to download and install Mukurtu.
```
mkdir mukurtu
cd mukurtu
ddev config --project-type=drupal --docroot=web
# Optional but recommended: install pdftotext inside the DDEV container:
echo "RUN sudo apt -qq update; sudo apt install poppler-utils -y;" > .ddev/web-build/Dockerfile.pdftotext
ddev start
ddev composer create-project mukurtu/mukurtu-template:dev-main
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
composer create-project mukurtu/mukurtu-template:dev-main .
```

**Note:** This template includes `drupal/devel` and `drupal/devel_php` in
`require-dev`, so they install by default unless you pass `--no-dev` to
`composer create-project`. Mukurtu no longer enables Devel automatically, so both
packages sit inert on disk until you turn them on. `devel_php` specifically provides
an execute-PHP capability, so enable it deliberately.

* Set your web server to serve the "web" folder (e.g. `mukurtu4/web`)
* Install Drupal as normal by opening the site in your web browser, the Mukurtu profile distribution will automatically be used.
