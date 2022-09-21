## Introduction

As you know, we need to import used PHP files using one of [`require`](https://www.php.net/manual/en/function.require.php),
[`include`](https://www.php.net/manual/en/function.include.php),
[`require_once`](https://www.php.net/manual/en/function.require-once.php) and
[`include_once`](https://www.php.net/manual/en/function.include-once.php) expressions.
This is a frustrating job to keep all imports in sync with file and directory changes.

This is the place that Saeghe comes to solve for you. You can write your PHP code, without considering file locations.
Then Saeghe will resolve and add them for you, either they are on your application or they come from another package.

## Usage

By running the following command, you can build your application for the `development` environment:

```shell
saeghe build
```

After running this command, you will have a clone of your application under `builds/development` directory.
When you run the build command, Saeghe uses your `saeghe.config.json` file and builds your application based on defined configs on this file.

> **Note**  
> Please read [configuration documentation](https://saeghe.com/documentations/customization) to customize you’re builds.

You can also build your application for the production environment like so:

```shell
saeghe build --environment=production
```

By running this command, you will see a built copy of your application in `builds/production` directory.

> **Note**  
> Currently, except build environment directory, there is no difference between `development` and `production` build.
> But soon there will come many cool features and boosts for your production code.

## What build means?

Let's say you have an application under `/var/www`.
Assume you defined a map as `"Application": "src"`
Consider the following code in your application:

```php
<?php

namespace Application;

use Application\SubDomain\ClassFoo;
use Exception;

class ClassBar extends ClassFoo
{

}

```

When you build your application, you are going to have a built copy of your file in the build environment like:

```php
<?php

namespace Application;

require_once '/var/www/src/SubDomain/ClassFoo.php';

use Application\SubDomain\ClassFoo;
use Exception;

class ClassBar extends ClassFoo
{
    ...
}

```

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

By having the same configuration as the previous example, When you build your project, you can expect the following file:

```php
<?php

namespace Applicaiton\SubDomain;

require_once '/var/www/src/SubDomain/ClassFoo.php';
require_once '/var/www/src/AnotherNamespace/ClassBaz.php';
require_once '/var/www/src/SampleFile.php';
require_once '/var/www/src/Helper.php';
require_once '/var/www/src/Constants.php';
require_once '/var/www/src/OtherConstants.php';
require_once '/var/www/Packages/owner-foo/package-foo/src/ClassInFoo.php';
require_once '/var/www/Packages/owner-bar/package-bar/src/SubDirectory/ClassInBar.php';
require_once '/var/www/Packages/owner-baz/package-baz/src/ClassInBaz.php';
require_once '/var/www/Packages/owner-baz/package-baz/src/AnotherClassInBaz.php';
require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Helper.php';
require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Constants.php';

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

As you guess, there is no more need for autoloading!
It increases the probability of using PHP's opcache and JIT in your application.
There are a lot of cool features that you can add to the build process.
