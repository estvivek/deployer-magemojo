<h1 align="center">
  <br>
    <img src="https://magemojo.com/magento/skin/frontend/b-responsive/magemojo/images/mojostratus.png" alt="Tradução Magento 2 pt_BR" width="530" height="201" title="MageMojo Deployer Recipe"/> 
  <br>
    MageMojo Stratus Deployer Recipe
  <br>
</h1>
<div align="center">
<a href="https://travis-ci.org/rafaelstz/deployer-magemojo"><img src="https://travis-ci.org/rafaelstz/deployer-magemojo.svg?branch=master" alt="Build Status"></a>
<a href="https://github.com/rafaelstz/deployer-magemojo/releases"><img src="https://img.shields.io/github/tag/rafaelstz/deployer-magemojo.svg" alt="Tags"></a>
<a href="https://packagist.org/packages/rafaelstz/deployer-magemojo"><img src="https://img.shields.io/packagist/dt/rafaelstz/deployer-magemojo.svg" alt="Total Downloads"></a>
<br><br>
</div>

Use this tool integrated with the [Deployer](https://deployer.org/) to use the power of [MageMojo Stratus CLI](https://magemojo.com/kb/knowledge-base/stratus-cli/).

If you are using Magento 2 you can use this [Magento 2 Deployer Recipe](https://github.com/rafaelstz/deployer-magento2) together!

Features
-----

You can run the command followed by **dep**. Example: `dep mm:cache:clear --stage=production`.

| Command | Description |
|----------|-------------|
| mm:autoscaling:reinit | Restart PHP-FPM |
| mm:cache:clear | Invalidate CloudFront cache and flush opcache, Redis, Varnish |
| mm:cloudfront:clear | Invalidate Cloudfront cache |
| mm:opcache:clear | Flush OPCache cache |
| mm:redis:clear | Clear Redis cache |
| mm:varnish:clear | Clear Varnish cache |
| mm:database:config | Get database configuration |
| mm:php:list | Show phpinfo options and values |
| mm:php:add | Add options and values to phpinfo |
| mm:php:remove | Remove options from phpinfo |

How to install
-------

How to install Deployer:

```
curl -LO https://deployer.org/deployer.phar && sudo mv deployer.phar /usr/local/bin/dep && sudo chmod +x /usr/local/bin/dep
```

How to install this package:

```
composer require rafaelstz/deployer-magemojo --dev
```

How to use
-----

After install it, you can add the line below after the **namespace** and run `dep` to check:

```php
// MageMojo Recipe
require __DIR__ . '/vendor/rafaelstz/deployer-magemojo/MageMojo.php';
```

To add an automatic process of all cache clean and restart all services, add these into the bottom:

```php
// MageMojo restart services & cache clear
after('success', 'mm:autoscaling:reinit');
after('success', 'mm:cache:clear');
```

For example:
-----

```php
<?php

namespace Deployer;
// MageMojo Recipe
require __DIR__ . '/vendor/rafaelstz/deployer-magemojo/MageMojo.php';

// Project
set('application', 'My Project Name');
set('repository', 'git@bitbucket.org:mycompany/my-project.git');
set('default_stage', 'production');

// Project Configurations
host('production')
    ->hostname('iuse.magemojo.com')
    ->user('my-user')
    ->port(22)
    ->set('deploy_path', '/home/my-project-folder')
    ->set('branch', 'master')
    ->stage('production');

// MageMojo restart services & cache clear
after('success', 'mm:autoscaling:reinit');
after('success', 'mm:cache:clear');

```

License
-----

MIT

[Rafael Correa Gomes](https://www.linkedin.com/in/rafaelcgstz/)
