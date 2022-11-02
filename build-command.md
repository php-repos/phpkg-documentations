## Introduction

As you know, we need to import used PHP files using one of
[`require`](https://www.php.net/manual/en/function.require.php),
[`include`](https://www.php.net/manual/en/function.include.php),
[`require_once`](https://www.php.net/manual/en/function.require-once.php) and
[`include_once`](https://www.php.net/manual/en/function.include-once.php) expressions.
This is a frustrating job to keep all imports in sync with file and directory changes.

This is the place that Saeghe comes to solve for you. You can write your PHP code, without considering file locations.
Then it resolve and add them for you, either they are on your application or they come from another package.

## Usage

By running the following command, you can build your application for the `development` environment:

```shell
saeghe build
```

After running this command, you will have a clone of your application under the `builds/development` directory.
When you run the build command, it uses your `saeghe.config.json` file
and builds your application based on the defined configs on this file.

> **Note**  
> Please read [configuration documentation](https://saeghe.com/documentations/customization)
> to learn how you can customize it.

You can also build your application for the production environment like so:

```shell
saeghe build production
```

By running this command, you will see a built copy of your application in the `builds/production` directory.

## What build means?

Let's say you have an application under `/var/www`.
Assume you defined a map as `"Application": "src"` and you defined your entry point to be at `public/index.php`
Consider the following code in your application:

```php
<?php

namespace Application;

use Application\SubDomain\ClassFoo;
use Exception;
use function Application\Str\between;
use const Application\Constants\CONSTANT_A;

class ClassBar extends ClassFoo
{

}

```

When you build your application, you are going to have a built copy of your file in the built environment like:

```php
<?php

namespace Application;

require_once '/var/www/src/Constants.php';
require_once '/var/www/src/Str.php';

use Application\SubDomain\ClassFoo;
use Exception;

class ClassBar extends ClassFoo
{
    ...
}

```

And you will see a map added to your `public/index.php` that tells to PHP how to find the `ClassFoo`.

Now let's make it more complicated. Consider this code:

```php
<?php

namespace Applicaiton\SubDomain;

use Application\SubDomain\ClassFoo;
use Application\AnotherNamespace\ClassBaz as Baz;
use function Application\SampleFile\anImportantFunction;
use function Application\HelperNamespace\helper1 as anotherFunction;
use const Application\Constants\CONSTANT;
use const Application\OtherConstants\RENAME as AnotherConstant;
use PackageFoo\ClassInFoo as AnotherFile, PackageBar\SubDirectory\ClassInBar;
use PackageBaz\SubDirectory\{ClassInBaz, AnotherClassInBaz as Another};
use function PackageFoo\SubDirectory\Helper\{helper1 as anotherFunction, helper2};
use const PackageBar\SubDirectory\Constants\{CONSTANT, RENAME as AnotherConstant};

class ClassBar extends ClassFoo
{
    ...
}

```

By having the same configuration as the previous example,
When you build your project, you can expect the following file:

```php
<?php

namespace Applicaiton\SubDomain;

require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Constants.php';
require_once '/var/www/src/Constants.php';
require_once '/var/www/src/OtherConstants.php';
require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Helper.php';
require_once '/var/www/src/SampleFile.php';
require_once '/var/www/src/Helper.php';

use Application\SubDomain\ClassFoo;
use Application\AnotherNamespace\ClassBaz as Baz;
use function Application\SampleFile\anImportantFunction;
use function Application\Helper\helper1 as anotherFunction;
use const Application\Constants\CONSTANT;
use const Application\OtherConstants\RENAME as AnotherConstant;
use PackageFoo\ClassInFoo as AnotherFile, PackageBar\SubDirectory\ClassInBar;
use PackageBaz\SubDirectory\{ClassInBaz, AnotherClassInBaz as Another};
use function PackageFoo\SubDirectory\Helper\{helper1 as anotherFunction, helper2};
use const PackageBar\SubDirectory\Constants\{CONSTANT, RENAME as AnotherConstant};

class ClassBar extends ClassFoo
{
    ...
}

```

And the map for used classes has been added to the `public/index.php`.

You can take advantage of both, `Functional` and `OOP` programming without thinking about files. 

