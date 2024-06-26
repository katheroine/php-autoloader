# Autoloader

![PHP workflow](https://github.com/ExOrg/php-autoloader/actions/workflows/php.yml/badge.svg)

Expansible Universal Autoloader.

## Getting Started

### Prerequisities

* [PHP](https://www.php.net/) 8.1 - 8.3
* [Git](https://git-scm.com/) 2.25.1+
* [Composer](https://getcomposer.org/) 2.6.0+

The instruction assumes using the Linux operating system or compatible tools for other operating systems.

### Installation

#### php8.*-cli, Git and Composer required

The recommended way to install Autoloader into the source code of the project is to handle it as code dependency by [Composer](http://getcomposer.org). [Git](https://git-scm.com/) is needed to fetch packages from version control repositories.

The *php8.\*-cli* is needed for installing Composer.

#### Autoloader installation

Add to your **composer.json** file appropriate entry by running the following command
```bash
composer require exorg/autoloader
```
If it's project set-up stage and no one dependency have been installed yet, run
```bash
composer install
```
If another dependencies have been intalled previously, run
```bash
composer update
```

## Usage

The simplest way to autoload all needed files in executable file is attaching *autoload.php* file generated by Composer (after running `composer install` or `composer update` command) like in following example

```php
require_once (__DIR__ . '/vendor/autoload.php');
```

### PSR-4 autoloader

```
.
└── src
    └── Subject
        └── Core
            └── SomeComponent.php
```

```php
<?php

namespace Vendor\Package\Subject\Core;

class SomeComponent
{

}

```

```php
<?php

declare(strict_types=1);

require_once (__DIR__ . '/vendor/autoload.php');

use ExOrg\Autoloader\Autoloader;
use ExOrg\Autoloader\Psr4AutoloadingStrategy;

$psr4Strategy = new Psr4AutoloadingStrategy();
$psr4Strategy->registerNamespacePath('Vendor\Package', './src');

$autoloader = new Autoloader();
$autoloader->setAutoloadingStrategy($psr4Strategy);
$autoloader->register();

$component = new Vendor\Package\Subject\Core\SomeComponent();

$autoloader->unregister();

```

### PSR-0 autoloader

```
.
└── src
    └── Vendor
        └── Package
            └── Subject
                └── Core
                    └── SomeComponent.php
```

```php
<?php

namespace Vendor\Package\Subject\Core;

class SomeComponent
{

}

```

```php
<?php

declare(strict_types=1);

require_once (__DIR__ . '/vendor/autoload.php');

use ExOrg\Autoloader\Autoloader;
use ExOrg\Autoloader\Psr0AutoloadingStrategy;

$psr0Strategy = new Psr0AutoloadingStrategy();
$psr0Strategy->registerNamespacePath('Vendor\Package', './src');

$autoloader = new Autoloader();
$autoloader->setAutoloadingStrategy($psr0Strategy);
$autoloader->register();

$component = new Vendor\Package\Subject\Core\SomeComponent();

$autoloader->unregister();

```

### PEAR autoloader

```
.
└── src
    └── Subject
        └── Core
            └── SomeComponent.php
```

```php
<?php

class Subject_Core_SomeComponent
{

}

```

```php
<?php

declare(strict_types=1);

require_once (__DIR__ . '/vendor/autoload.php');

use ExOrg\Autoloader\Autoloader;
use ExOrg\Autoloader\PearAutoloadingStrategy;

$pearStrategy = new PearAutoloadingStrategy();
$pearStrategy->registerPseudonamespacePath('Subject', './src');

$autoloader = new Autoloader();
$autoloader->setAutoloadingStrategy($pearStrategy);
$autoloader->register();

$component = new Subject_Core_SomeComponent();

$autoloader->unregister();

```

### Fixed autoloader

```
.
└── src
    └── Subject
        └── Core
            └── SomeComponent.php
```

```php
<?php

namespace Subject\Core;

class SomeComponent
{

}

```

```php
<?php

declare(strict_types=1);

require_once (__DIR__ . '/vendor/autoload.php');

use ExOrg\Autoloader\Autoloader;
use ExOrg\Autoloader\FixedAutoloadingStrategy;

$fixedStrategy = new FixedAutoloadingStrategy();
$fixedStrategy->registerClassPath('Subject\Core\SomeComponent', './src/Subject/Core/SomeComponent.php');

$autoloader = new Autoloader();
$autoloader->setAutoloadingStrategy($fixedStrategy);
$autoloader->register();

$component = new \Subject\Core\SomeComponent();

$autoloader->unregister();

```

### Recursive autoloader

```
.
└── src
    └── Subject
        └── Core
            └── SomeComponent.php
```

```php
<?php

namespace Subject\Core;

class SomeComponent
{

}

```

```php
<?php

declare(strict_types=1);

require_once (__DIR__ . '/vendor/autoload.php');

use ExOrg\Autoloader\Autoloader;
use ExOrg\Autoloader\RecursiveAutoloadingStrategy;

$recursiveStrategy = new RecursiveAutoloadingStrategy();
$recursiveStrategy->registerPath('./src');

$autoloader = new Autoloader();
$autoloader->setAutoloadingStrategy($recursiveStrategy);
$autoloader->register();

$component = new \Subject\Core\SomeComponent();

$autoloader->unregister();

```

## Tests

### Unit tests

This project has unit tests, which has been built with [PHPUnit](https://phpunit.de/) framework and run on Linux operating system.

To run tests, write the following command in your command line inside the main Autoloader project directory

```bash
vendor/bin/phpunit tests/
```

or use a Composer script

```bash
composer test
```

### Code style tests

This code follows [PSR-1](http://www.php-fig.org/psr/psr-1/) and [PSR-12](http://www.php-fig.org/psr/psr-12/) standards.

To run tests for code style write the following command in your command line inside the main Autoloader project directory

```bash
vendor/bin/phpcs tests/ src/
```

or use a Composer script

```bash
composer sniff
```

You can also use a Composer script for running both tests and check code style

```bash
composer check
```

## Built with

* [Linux Mint](https://www.linuxmint.com/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [PHPUnit](https://phpunit.de/)
* [PHPCodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
* [Composer](https://getcomposer.org/)
* [Git](https://git-scm.com/)
* [GitHub](https://github.com/)

## Versioning

This project is versioning according to [SemVer](http://semver.org/)  versioning standars. All available [releases](https://github.com/ExOrg/php-autoloader/releases) are [tagged](https://github.com/ExOrg/php-autoloader/tags).

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on the code of conduct, and the process for submitting pull requests.

## Author

* **Katarzyna Krasińska** - [katheroine](https://github.com/katheroine), [ExOrg](https://github.com/ExOrg)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
