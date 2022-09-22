## Introduction

Saeghe is a modern PHP package manager. You can simply use it to manage your package dependencies and your codebase.
Saeghe finds your required PHP files, from your codebase or your application's dependencies, and adds them to your code.

### Improve performance

Saeghe helps you to improve your application's performance.
It is not going to use any autoloading, instead, it is going to inject the `require` statements for
your files directly into PHP files. It is much faster than autoloading the classes.

You can see the benchmark table on [saegh benchmark repository](https://github.com/saeghe/benchmark)

Also, you can clone the benchmark repository and play with it by yourself.
Follow the `README` instruction on the benchmark repository.

## Requirements

For installing Saeghe, you need to have git installed on your machine as well as PHP version >= 8.0

## Installation

You can simply install Saeghe by running the following command in your terminal:

```shell
sh -c "$(curl -fsSL https://raw.github.com/saeghe/installation/master/install.sh)"
```

By running this command, Saeghe will be installed on your home directory.

Now Saeghe is ready to use.

## Usage

### Initialize your application
Using Saeghe is very easy. First, make your application's directory and change your current directory to it:

```shell
mkdir my-application && cd my-application
```

Next run Saeghe `init` command to create the required files and directories:

```shell
saeghe init
```

> **Note**  
> For more information about init command, check its [documentation](http://saeghe.com/documentations/init-command).

Now you will see two added directories, `builds` and `Packages`.
Saeghe will use the `Packages` directory to keep your added package’s source files.
The `builds` directory will be used by Saeghe when you run the `build` command that we will explain later.

Also, you will see two new files added to your application.
`Saeghe.config.json` and `saeghe.config-lock.json`.
The `Saeghe.config.json` is for keeping your application's configuration.

The default content for this file should be:

```json
{
    "map": [],
    "entry-points": [],
    "excludes": [],
    "executables": [],
    "packages-directory": "Packages",
    "packages": []
}
```

> **Note**  
> For more information about configurations, please check [customization documentation](http://saeghe.com/documentations/customization).

The `saeghe.config-lock.json` file will be used for keeping metadata about added packages.

> **Note**  
> For more information about adding packages, please check [add command documentation](http://saeghe.com/documentations/add-command).

### Add your application's map

The next step is to define your map.
Assume you want to keep your application files in the `src` directory and have a `tests` directory to add your tests into it.
You need to define your map configuration inside the `saeghe.config.json` file as follows:
```json
{
  "map": {
    "Application": "src",
    "Tests": "tests"
  },
  "entry-points": [],
  "excludes": [],
  "executables": [],
  "packages-directory": "Packages",
  "packages": []
}
```
By this configuration, you ask Saeghe, to map any use statements starting with `Application` to `src` directory
and any use statement starting with `Tests` to your `tests` directory.

We are going to explain more about mapping in examples.

### Adding packages

For adding any packages to your application you can use the `add` command.
For example, if you want to use the `test-runner` package, you can simply copy its URL from GitHub and run the following command:

```shell
saegh add --package=https://github.com/saeghe/test-runner.git
```

After running this command, there will be three changes in your application:
- Test runner source code will be added under the `Packages` directory.
- Test runner path and installed version will be added to your `saeghe.config.json` file.
- Test runner metadata will be added to your `saeghe.config-lock.json` file.

So far, if you did similar steps, your `saeghe.config.json` file should be like this:
```json
{
  "map": {
    "Application": "src",
    "Tests": "tests"
  },
  "entry-points": [],
  "excludes": [],
  "executables": [],
  "packages-directory": "Packages",
  "packages": {
    "https:\/\/github.com\/saeghe\/test-runner.git": "installed-version"
  }
}
```

And your `saeghe.config-lock.json` file should be something like:

```json
{
    "packages": {
        "git@github.com:saeghe\/test-runner.git": {
            "version": "installed-version",
            "hash": "installed-commit-hash",
            "owner": "saeghe",
            "repo": "test-runner"
        }
    }
}
```
> **Note**  
> For more information about adding packages and versioning, please check [add command documentation](http://saeghe.com/documentations/add-command).

### Build your code for the development

When you are ready to run and test your application, you need to build your files using Saeghe's `build` command.
For doing this, you should run:

```shell
saeghe build
```

By running this command, Saeghe will make a `development` directory under your `builds` directory and then starts to build your application into it.

> **Note**  
> For more information about the build command, please check [build command documentation](http://saeghe.com/documentations/build-command).

For example, assume you have two PHP files in your application.

First, a controller file under the `src` directory named `MyController.php` with contents as:

```php
<?php

namespace Application;

use Application\Model\User;

class MyController
{
    
}

```
And another `User.php` file in the `src\Models` directory:

```php
<?php

namespace Application\Models;

class User
{

}

```

Now, if you run the `build` command, you should see these changes:

Under `builds/development/src/MyController.php`:

```php
<?php

namespace Application;

require_once '{ABSOLUTE_PATH_TO_src_DIRECTORY}/Models/User.php';

use Application\Model\User;

class MyController
{
    
}

```

And in `builds/development/src/Models/User.php`:

```php
<?php

namespace Application\Models;

class User
{

}

```

There are no changes for the `User.php` file since there are no use statements in this file.

Use can use the `build` command, to build files containing any kind of use statement.

> **Note**  
> For more information about use statements, please check [PHP use statements](https://www.php.net/manual/en/language.namespaces.importing.php).

### Build for production

When your application has been ready, you can build the application for the production environment.
You can use the `build` command like the following:

```shell
saeghe build --environment=production
```

This command will make a `production` directory under your `builds` directory and builds your application into it.

> **Note**  
> For more information about `build`, please check [build documentations](https://saeghe.com/documentations/build-command).

## Migrate from composer

If you have a package or application that uses composer as the package manager,
you can use the following command to migrate from composer to Saeghe:

```shell
saeghe migrate
```

> **Note**  
> For more information about migration, please check [migrate documentations](https://saeghe.com/documentations/migrate-command).
