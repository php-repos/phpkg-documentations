## Introduction

Saeghe is a modern PHP package manager. You can simply manage your package dependencies and your codebase.
It detects your required PHP files from your codebase and your application's dependencies.
Then adds them to your code.
This way you can take advantage of both; `Functional` and `OOP` programming.
It works with git directly. It means there is no need for any intermediate repository registration.

## Requirements

For installing it, you need to have git installed on your machine as well as PHP version >= 8.1
with `php-mbstring`, `php-zip` and `php-curl` extensions installed.

## Installation

You can simply install Saeghe by running the following command in your terminal:

```shell
bash -c "$(curl -fsSL https://raw.github.com/saeghe/installation/master/install.sh)"
```

By running this command, it will be installed on your home directory.
> **Note**
> You need to open a new terminal to get access to the new path.

## Add GitHub token

A GitHub token is required to read repositories. 
If you already have an environment variable named `GITHUB_TOKEN` with your GitHub token, then you don't need to do anything. 
But in case you don't have this environment variable, you need to set one using the `credential` command.
You can generate a token by following this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). 
Then you can use the following command to add it to credentials:

```shell
saeghe credential github.com {your-github-token}
```

Now it is ready to use.

## Usage

### Initialize your application

First, make your application's directory and change your current directory to it:

```shell
mkdir my-application && cd my-application
```

Next run the `init` command to create the required files and directories:

```shell
saeghe init
```

> **Note**  
> For more information about init command, check its [documentation](http://saeghe.com/documentations/init-command).

Now you will see two added directories, `builds` and `Packages`.
The `Packages` directory gets used to keep your added package’s source files.
The `builds` directory will be used when you run the `build` command we will explain later.

Also, you will see two new files added to your application.
`saeghe.config.json` and `saeghe.config-lock.json`.
The `saeghe.config.json` is for keeping your application's configuration.

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
> For more information about configurations,
> please check [customization documentation](http://saeghe.com/documentations/customization).

The `saeghe.config-lock.json` file will be used for keeping metadata about added packages.

> **Note**  
> For more information about adding packages,
> please check [add command documentation](http://saeghe.com/documentations/add-command).

### Add your application's map

The next step is to define your map.
Assume you want to keep your application files in the `src` directory
and have a `tests` directory to add your tests into it.
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

By this configuration, it maps any used namespace starting with `Application` to the `src` directory
and any used namespaces starting with `Tests` to your `tests` directory.

We are going to explain more about mapping in examples.

### Adding packages

For adding any packages to your application you can use the `add` command.
For example, if you want to use the `test-runner` package,
you can simply copy its URL from GitHub and run the following command:

```shell
saeghe add https://github.com/saeghe/test-runner.git
```

As you see, there is no intermediate repository website for packages, you can directly use their git URL.

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

And your `saeghe.config-lock.json` file should be something like this:

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
> For more information about adding packages and versioning,
> please check [add command documentation](http://saeghe.com/documentations/add-command).

### Add your entry points

The required code for autoloading used classes gets added automatically to your entry point files.
For example, let's say your entry point is in the `public/index.php` file.
Then by adding this file to the entry points config in the `saeghe.config.json` file,
it adds the required map and code for autoloading to these files.

```json
{
  "map": {
    "Application": "src",
    "Tests": "tests"
  },
  "entry-points": ["public/index.php"],
  "excludes": [],
  "executables": [],
  "packages-directory": "Packages",
  "packages": {
    "https:\/\/github.com\/saeghe\/test-runner.git": "installed-version"
  }
}
```

### Build your code for the development

When you are ready to run and test your application, you need to build your files using the `build` command.
For doing this, you should run:

```shell
saeghe build
```

By running this command, it makes a `development` directory
under your `builds` directory and then starts to build your application into it.

> **Note**  
> For more information about the build command,
> please check [build command documentation](http://saeghe.com/documentations/build-command).

For example, assume you have two PHP files in your application.

First, a controller file under the `src` directory named `MyController.php` with contents as:

```php
<?php

namespace Application;

use Application\Model\User;
use function Application\Helper\my_helper;
use const Application\Constants\MY_CONST;

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

require_once '{ABSOLUTE_PATH_TO_src_DIRECTORY}/Constants.php';
require_once '{ABSOLUTE_PATH_TO_src_DIRECTORY}/Helper.php';

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

The required map for autoloading used classes also has been added to the `build/development/public/index.php` file.

Use can use the `build` command, to build files containing any kind of use statement.

> **Note**  
> For more information about use statements,
> please check [PHP use statements](https://www.php.net/manual/en/language.namespaces.importing.php).

### Developing

While you are developing your application,
you are going to constantly add and remove files to your project and test the application.
Running the `build` command for each change and test is not optimal.

There is a `watch` command that you can run:

```shell
saeghe watch
```

> **Note**  
> For more information about `watch`,
> please check [watch documentation](https://saeghe.com/documentations/watch-command).

### Build for production

When your application has been ready, you can build the application for the production environment.
You can use the `build` command like the following:

```shell
saeghe build production
```

This command will make a `production` directory under your `builds` directory and builds your application into it.

> **Note**  
> For more information about `build`,
> please check [build documentation](https://saeghe.com/documentations/build-command).

## Migrate from composer

If you have a package or application that uses composer as the package manager,
you can use the following command to migrate from composer:

```shell
saeghe migrate
```

> **Note**  
> For more information about migration,
> please check [migrate documentation](https://saeghe.com/documentations/migrate-command).
