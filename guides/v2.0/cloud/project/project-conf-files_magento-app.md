---
layout: default
group: cloud
subgroup: 100_project
title: .magento.app.yaml
menu_title: .magento.app.yaml
menu_order: 50
menu_node: 
version: 2.0
github_link: cloud/project/project-conf-files_magento-app.md
---

## About `.magento.app.yaml` {#cloud-yaml-platform}
Magento Enterprise Cloud Edition supports multiple applications per project but typically, a project is composed of a single application, in which case you can simply put a `.magento.app.yaml` at the root of your repository.

This file controls the application and the way it is built and deployed on Magento Enterprise Cloud Edition.

[Sample `.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml){:target="_blank"}

<div class="bs-callout bs-callout-info" id="info">
  <p>Changes you make using <code>.yaml</code> files affect your <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-int">integration environment</a> only. For technical reasons, neither <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-stage">staging</a> nor <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-prod">production</a> environments use <code>.yaml</code> files. To make these changes in a staging or production environment, you must create a <a href="{{ page.baseurl }}cloud/welcome/get-help.html">Support ticket</a>.</p>
</div>

The following sections discuss properties in `.magento.app.yaml`.

## Defaults {#cloud-yaml-default}
`.magento.app.yaml` has many default values; see the [sample `.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml){:target="_blank"}.

## `name` property {#name}
`name` identifies the application in the project. Magento Enterprise Cloud Edition
supports multiple applications in a project, so each application
must have a *unique name* in a project. 

{% collapsible name property: %}

`name` can consist only of lower case alphanumeric characters; that is, `a`&ndash;`z` and `0`&ndash;`9`. `name`
is used in the [`routes.yaml`]({{page.baseurl}}cloud/project/project-conf-files_routes.html) to define the HTTP upstream
(by default, `php:php`). 

For example, if the value of `name` is `app`, you must use `app:php` in the upstream field. You can also use this name in multi-application relationships.

<div class="bs-callout bs-callout-info" id="info">
  <p>If you change the name you should think about updating your other configuration files (<code>routes.yaml</code> or the different <code>.magento.app.yaml</code>, you will have in a multi-application project. Changing the name has no effect on your different services (such as databases).</p>
</div>

{% endcollapsible %}

## `type` and `build` {#cloud-yaml-platform-type}
The `type`  and `build` properties are used to build and run the project. The only supported `type` currently is {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}.

Supported versions:

    type: php:5.5
    type: php:5.6
    type: php:7.0

The `build` determines what happens by default when building the project. The only value currently supported is `composer`.

Example:

    type: php:5.6
    build:
        flavor: composer

## `access` {#cloud-yaml-platform-access}
`access` defines the user roles who can log in using SSH to the
environments to which they have access.

{% collapsible access property %}

Possible values are:

	ssh: admin
	ssh: contributor
	ssh: viewer

{% endcollapsible %}

## `relationships`  {#cloud-yaml-platform-rel}
`relationships` defines how services are mapped in your
application.

{% collapsible relationships %}

The left-hand side is the name of the relationship as it will be exposed
to the application in the `MAGENTO_CLOUD_RELATIONSHIPS` environment
variable. The right-hand side is in the form
`<service name>:<endpoint name>`, where `<service name>` comes from 
 `.magento/services.yaml` and  `<endpoint name>` should be the same as the
 value of `type`  declared in that same file.

Example of valid options are:

	database: "mysql:mysql"
	database2: "mysql2:mysql"
	cache: "arediscache:redis"
	search: "searchengine:solr"

See also [`services.yaml` documentation]({{page.baseurl}}cloud/project/project-conf-files_services.html) for a full list of currently supported service types and endpoints.

{% endcollapsible %}

## `web` {#cloud-yaml-platform-web}
`web` defines how your application is exposed to the web (in HTTP). Here we tell the web application how to serve content, from the front-controller script to a non-static request to an `index.php` file on the root. We support any directory structure so the static file can be in a sub directory, and the `index.php` file can be further down.

{% collapsible web %}

`web` supports the following:

-   `document_root`: The path relative to the root of the application
    that is exposed on the web. Typical values include `/public` and `/web`.
-   `passthru`: The URL used in the event a static file or PHP file could not be found. This would typically be your applications front controller, often `/index.php` or `/app.php`.
-   `index_files`: To use a static file (for example, `index.html`) to serve
    your application. This key expects a collection. 

    For this to
    work, the static file(s) should be included in your whitelist. For example,
    to use a file named `index.html` as an index file, your whitelist should
    include an element that matches the filename, like `- \.html$`.
-   `blacklist`: A list of files that should never be executed. Has no effect on static files.
-   `whitelist`: A list of static files (as regular expressions) that can be served. Dynamic files (for example, PHP files) are treated as static files and have their source code served, but they are not executed.
-   `expires`: The number of seconds whitelisted (that is, static) content
    should be cached by the browser. This enables the cache-control and
    Expires headers for static content. The `expires` directive and
    resulting headers are left out entirely if this isn't set.

Contrary to standard `.htaccess` approaches, which accept a
*blacklist* and allow everything to be accessed except a specific
list, we accept a *whitelist*, which means that anything not matched
will trigger a 404 error and will be passed through to your `passthru`
URL.

Our default configuration allows the following:

*   From the root (`/`) path, only web, media, and `robots.txt` files can be accessed
*   From the `/pub/static` and `/pub/media` paths, any file can be accessed

{% endcollapsible %}

## `disk` {#cloud-yaml-platform-disk}
`disk` defines the size of the persistent disk size of the
application in MB.

<div class="bs-callout bs-callout-info" id="info">
  <p>The minimal recommended disk size is 256MB. If you see the error <code>UserError: Error building the project: Disk size may not be smaller than 128MB</code>, increase the size to 256MB.</p>
</div>

## `mounts` {#cloud-yaml-platform-mounts}
`mounts` is an object whose keys are paths relative to the root of
the application. It's in the form `volume_id[/subpath]`.

{% collapsible mounts property %}

The format is:

	"/public/sites/default/files": "shared:files/files"

<div class="bs-callout bs-callout-info" id="info">
  <p><code>shared</code> means that the volume is shared between your applications inside an environment. The <code>disk</code> key defines the size available for that <code>shared</code> volume.</p>
</div>

{% endcollapsible %}

## `dependencies` {#cloud-yaml-platform-dep}
`dependencies` enables you to specify dependencies that your
application might need during the build process.

{% collapsible dependencies property %}

Magento Enterprise Cloud Edition supports dependencies on the following
languages:

*	PHP
*	Ruby
*	NodeJS

Those dependencies are independent of the eventual dependencies of your
application, and are available in the `PATH`, during the build process
and in the runtime environment of your application.

You can specify those dependencies as follows:

	ruby:
	   sass: "~3.4"
	nodejs:
	   grunt-cli: "~0.3"

{% endcollapsible %}

## `hooks` {#cloud-yaml-platform-hooks}
The `hooks` (also referred to as `deployment hooks`) enable you to define shell
commands to run during the deployment process.

They can be executed at various points in the lifecycle of the
application.

{% collapsible hooks property %}

Possible hooks are:

-   `build`: We run build hooks before your application has been
    packaged. No other services (such as the database, or redis) are accessible at this time since the
    application has not been deployed yet.
-   `deploy`: We run deploy hooks after your application has been
    deployed and started. You can access other services at this point.

To add additional hooks (such as CLI commands that are offered by a custom extension), add them under the `build` or
`deploy` sections as follows:

{% highlight yaml %}
hooks:
    build: |
        php ./bin/magento magento-cloud:build
        php ./bin/magento additional:build:hook
    deploy: |
        php ./bin/magento magento-cloud:deploy
        php ./bin/magento additional:deploy:hook
{% endhighlight %}

The home directory, where your application is mounted, is `/app`, and that is the directory from which hooks will be
run unless you `cd` somewhere else.

The hooks fail if the final command in them fails. To
cause them to fail on the first failed command, add `set -e` to the beginning
of the hook.

#### [Example] Compile SASS files using grunt
For example, to compile SASS files using grunt:

{% highlight xml %}
dependencies:
  ruby:
    sass: "3.4.7"
  nodejs:
    grunt-cli: "~0.1.13"

hooks:
  build: |
    cd public/profiles/project_name/themes/custom/theme_name
    npm install
    grunt
{% endhighlight %}

{% endcollapsible %}

## `crons` {#cloud-yaml-platform-cron}
`crons` describes processes that are triggered on a
schedule.

{% collapsible More information about crons: %}

`crons` supports the following:

*	`spec`: The cron specification. The minimum interval is once per 5 minutes.
*	`cmd`: The command to execute.

A sample Magento cron job follows:

	crons:
    cronrun:
        spec: "*/5 * * * *"
        cmd: "php bin/magento cron:run"
        
{% endcollapsible %}

## Configure PHP options {#cloud-yaml-platform-php}
You can choose which version of PHP you want to run in your `.magento.app.yaml` file.:

{% highlight yaml %}
name: myphpapp
type: php:5.6
{% endhighlight %}

We support PHP versions 5.5, 5.6, and 7.0. The default is 7.0.

See one of the following sections for more information:

*   [PHP extensions](#cloud-yaml-platform-php-ext)
*   [Customize `php.ini` settings](#cloud-yaml-platform-php-set)

### PHP extensions {#cloud-yaml-platform-php-ext}
You can define additional PHP extensions you want to enable or disable. Example:

{% highlight yaml %}
# .magento.app.yaml
runtime:
    extensions:
        - xdebug
        - redis
        - ssh2
    disabled_extensions:
        - sqlite3
{% endhighlight %}

To view the current list of PHP extensions, SSH into your environment and enter the following command:

	php -m

Magento requires the following PHP extensions that are enabled by default: 

*	<a href="http://php.net/manual/en/book.curl.php" target="_blank">curl</a>
*	<a href="http://php.net/manual/en/book.image.php" target="_blank">gd</a>
*	<a href="http://php.net/manual/en/book.intl.php" target="_blank">intl</a>
*	PHP 7 only: 

	*	[json](http://php.net/manual/en/book.json.php){:target="_blank"}
	*	[iconv](http://php.net/manual/en/book.iconv.php){:target="_blank"}
*	<a href="http://php.net/manual/en/book.mcrypt.php" target="_blank">mcrypt</a>
*	<a href="http://php.net/manual/en/ref.pdo-mysql.php" target="_blank">PDO/MySQL</a>
*	<a href="http://php.net/manual/en/book.bc.php" target="_blank">bc-math</a> 
*	<a href="http://php.net/manual/en/book.mbstring.php" target="_blank">mbstring</a>
*	<a href="http://php.net/manual/en/book.mhash.php" target="_blank">mhash</a>
*	<a href="http://php.net/manual/en/book.openssl.php" target="_blank">openssl</a>
*	<a href="http://php.net/manual/en/book.simplexml.php" target="_blank">SimpleXML</a>
*	<a href="http://php.net/manual/en/book.soap.php" target="_blank">soap</a>
*	<a href="http://php.net/manual/en/book.xml.php" target="_blank">xml</a>
*	<a href="http://php.net/manual/en/book.zip.php" target="_blank">zip</a>
 
You must install the following extensions:

*   <a href="http://php.net/manual/en/book.imagick.php" target="_blank">ImageMagick 6.3.7</a> (or later)

    imagick can optionally be used with the `gd` extension
*	<a href="http://php.net/manual/en/book.xsl.php" target="_blank">xsl</a>
*	[redis](https://pecl.php.net/package/redis){:target="_blank"}

In addition, we strongly recommend you enable `opcache`. 

Other PHP extensions you can optionally install:

*	[apcu](http://php.net/manual/en/book.apcu.php){:target="_blank"}
*	[blackfire](https://blackfire.io/docs/up-and-running/installation){:target="_blank"}
*	[enchant](http://php.net/manual/en/book.enchant.php){:target="_blank"}
*	[gearman](http://php.net/manual/en/book.gearman.php){:target="_blank"}
*	[geoip](http://php.net/manual/en/book.geoip.php){:target="_blank"}
*	[imap](http://php.net/manual/en/book.imap.php){:target="_blank"}
*	[pecl-http](https://pecl.php.net/package/pecl_http){:target="_blank"}
*	[pinba](http://pinba.org){:target="_blank"}
*	[propro](https://pecl.php.net/package/propro){:target="_blank"}
*	[pspell](http://php.net/manual/en/book.pspell.php){:target="_blank"}
*	[raphf](https://pecl.php.net/package/raphf){:target="_blank"}
*	[readline](http://php.net/manual/en/book.readline.php){:target="_blank"}
*	[recode](http://php.net/manual/en/book.recode.php){:target="_blank"}
*	[snmp](http://php.net/manual/en/book.snmp.php){:target="_blank"}
*	[sqlite3](http://php.net/manual/en/book.sqlite3.php){:target="_blank"}
*	[ssh2](http://php.net/manual/en/book.ssh2.php){:target="_blank"}
*	[tidy](http://php.net/manual/en/book.tidy.php){:target="_blank"}
*	[xcache](https://xcache.lighttpd.net){:target="_blank"}
*	[xdebug](https://xdebug.org){:target="_blank"}
*	[xhprof](http://php.net/manual/en/book.xhprof.php){:target="_blank"}
*	[xmlrpc](http://php.net/manual/en/book.xmlrpc.php){:target="_blank"}

### Customize `php.ini` settings {#cloud-yaml-platform-php-set}
You can also create and push a `php.ini` file that is appended to
the configuration maintained by Magento Enterprise Cloud Edition.

In your repository, the `php.ini` file should be added to the root of
the application (the repository root).

<div class="bs-callout bs-callout-warning">
    <p>Configuring PHP settings improperly can cause issues. We recommend only advanced administrators set these options.</p>
</div>

For example, if you need to increase the PHP memory limit:

	memory_limit = 756M

For a list of recommended PHP configuration settings, see [Required PHP settings]({{ page.baseurl }}install-gde/prereq/php-settings.html).

After pushing your file, you can check that the custom PHP configuration
has been added to your environment by [creating an SSH tunnel]({{page.baseurl}}cloud/env/environments-start.html#env-start-tunn) to your environment and entering:

	cat /etc/php5/fpm/php.ini

#### Related topics
*	[Get started with a project]({{page.baseurl}}cloud/project/project-start.html)
*	[routes.yaml]({{page.baseurl}}cloud/project/project-conf-files_routes.html)
*	[services.yaml]({{page.baseurl}}cloud/project/project-conf-files_services.html)
