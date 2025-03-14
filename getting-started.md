## Introduction

phpkg is a modern PHP package manager that is ideal for developers working on projects that require functional 
and object-oriented programming. 
It allows you to easily manage your package dependencies using `phpkg` in your codebase.
It detects your required PHP files from your codebase and your application's dependencies, and then adds them to your code. 
It works with git repositories directly, meaning there is no need for any intermediate repository registration.

## Requirements

For installing it, you need to have `unzip` and git installed on your machine as well as PHP version >= 8.1
with `php-zip` and `php-curl` extensions installed.

## Installation

> **Note**  
> These installer work on Unix/Linux and macOS systems. Support for windows will be added soon.

You can simply install `phpkg` by running the following command in your terminal:

```shell
bash -c "$(curl -fsSL https://raw.github.com/php-repos/phpkg-installation/master/install.sh)"
```

By running this command, `phpkg` will be installed on your home directory.

> **Note**
> You need to open a new terminal to get access to the new added path.

## Add GitHub token

A GitHub token is required to read private repositories. 
If you already have an environment variable named `GITHUB_TOKEN` with your GitHub token, then you don't need to do anything. 
But in case you don't have this environment variable, you need to set one using the `credential` command.
You can generate a token by following this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). 
Then you can use the following command to add it to credentials:

```shell
phpkg credential github.com {your-github-token}
```

Now it is ready to use.

## Usage

With `phpkg`, you can easily manage dependencies for your projects during development by installing and updating 
the necessary libraries and packages with just a few simple commands. 

For example, to install a package called "mypackage" from a git repository, you can run the following command:

```shell
phpkg add https://github.com/myuser/mypackage
```

Additionally, it also allows for running standalone packages,
making it easy for you to execute any PHP applications or scripts with just one command.
for example, to run a package called "mypackage", you can run the following command:

```shell
phpkg run mypackage-git-url
```

You should expect to see the package's output displayed in the terminal.

You can also serve a standalone phpkg application and access its entry point in a web browser of your choice.
For serving an application, you can run the following command:

```shell
phpkg serve application-git-url
```

### Use as a package manager

#### Initialize your application

First, make your application's directory and change your current directory to it:

```shell
mkdir my-application && cd my-application
```

Next run the `init` command to create the required files and directories:

```shell
phpkg init
```

> **Note**  
> For more information about init command, check its [documentation](https://phpkg.com/documentations/init-command).

Now you will see a `Packages` directory added to your project.
The `Packages` directory gets used to keep your added package’s source files.

Also, you will see two new files added to your application.
`phpkg.config.json` and `phpkg.config-lock.json`.
The `phpkg.config.json` is for keeping your application's configuration.

The default content for this file should be:

```json
{
  "map": [],
  "autoloads": [],
  "excludes": [],
  "entry-points": [],
  "executables": [],
  "import-file": "phpkg.imports.php",
  "packages-directory": "Packages",
  "packages": []
}
```

> **Note**  
> For more information about configurations,
> please check [customization documentation](https://phpkg.com/documentations/customization).

The `phpkg.config-lock.json` file will be used for keeping metadata about added packages.

> **Note**  
> For more information about adding packages,
> please check [add command documentation](https://phpkg.com/documentations/add-command).

#### Add your application's map

The next step is to define your map.
Assume you want to keep your application files in the `src` directory
and have a `tests` directory to add your tests into it.
You need to define your map configuration inside the `phpkg.config.json` file as follows:

```json
{
  "map": {
    "Application": "src",
    "Tests": "tests"
  },
  "autoloads": [],
  "excludes": [],
  "entry-points": [],
  "executables": [],
  "import-file": "phpkg.imports.php",
  "packages-directory": "Packages",
  "packages": []
}
```

By this configuration, `phpkg` maps any used namespace starting with `Application` to the `src` directory
and any used namespaces starting with `Tests` to your `tests` directory.

Later on the example, you will see how `phpkg` uses this map.

#### Adding packages

For adding any packages to your application you can use the `add` command.
For example, if you want to use the `test-runner` package,
you can simply copy its URL from GitHub and run the following command:

```shell
phpkg add https://github.com/php-repos/test-runner.git
```

As you see, there is no intermediate repository website for packages, you can directly use their git URL.

After running this command, there will be three changes in your application:
- Test runner source code will be added under the `Packages` directory.
- Test runner path and installed version will be added to your `phpkg.config.json` file.
- Test runner metadata will be added to your `phpkg.config-lock.json` file.

So far, if you did similar steps, your `phpkg.config.json` file should be like this:

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
    "https:\/\/github.com\/php-repos\/test-runner.git": "installed-version"
  }
}
```

And your `phpkg.config-lock.json` file should be something like this:

```json
{
    "packages": {
        "git@github.com:php-repos\/test-runner.git": {
            "version": "installed-version",
            "hash": "installed-commit-hash",
            "owner": "php-repos",
            "repo": "test-runner"
        }
    }
}
```

> **Note**  
> For more information about adding packages and versioning,
> please check [add command documentation](https://phpkg.com/documentations/add-command).

#### Add your entry points

The required code for autoloading used classes gets added automatically to your entry point files.
For example, let's say your entry point is in the `public/index.php` file.
Then by adding this file to the entry points config in the `phpkg.config.json` file,
`phpkg` adds the required code for autoloading to these files.

```json
{
  "map": {
    "Application": "src",
    "Tests": "tests"
  },
  "autoloads": [],
  "excludes": [],
  "entry-points": ["public/index.php"],
  "executables": [],
  "import-file": "phpkg.imports.php",
  "packages-directory": "Packages",
  "packages": {
    "https:\/\/github.com\/php-repos\/test-runner.git": "installed-version"
  }
}
```

#### Build your code for the development

When you are ready to run and test your application, you need to build your files using the `build` command.
For doing this, you should run:

```shell
phpkg build
```

By running this command, it makes a `development` directory
under a `builds` directory and then starts to build your application into it.

> **Note**  
> For more information about the build command,
> please check [build command documentation](https://phpkg.com/documentations/build-command).

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

Now, if you run the `build` command, you should see these:

Under `builds/development/src/MyController.php`:

```php
<?php

namespace Application;

require_once '{ABSOLUTE_PATH_TO_src_DIRECTORY}/Constants.php';
require_once '{ABSOLUTE_PATH_TO_src_DIRECTORY}/Helper.php';

use Application\Model\User;
use function Application\Helper\my_helper;
use const Application\Constants\MY_CONST;

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

The required map for autoloading used classes also has been added to the `build/development/public/index.php` 
that you defined as an entry point.

You can use the `build` command, to build files containing any kind of use statement.

> **Note**  
> For more information about use statements,
> please check [PHP use statements](https://www.php.net/manual/en/language.namespaces.importing.php).

#### Continues Development

While you are developing your application,
you are going to constantly add and remove files to your project and test the application.
Running the `build` command for each change and test is not optimal.

There is a `watch` command that you can run:

```shell
phpkg watch
```

> **Note**  
> For more information about `watch`,
> please check [watch documentation](https://phpkg.com/documentations/watch-command).

#### Build for production

When your application has been ready, you can build the application for the production environment.
You can use the `build` command like the following:

```shell
phpkg build production
```

This command will make a `production` directory under your `builds` directory and builds your application into it.

> **Note**  
> For more information about `build`,
> please check [build documentation](https://phpkg.com/documentations/build-command).

### Use as an application runner

You can use `phpkg` to run any runnable package, which means a package that has an entry point file.
This feature is useful for developers who want to run small, stand-alone scripts or programs.
For example, you can find 2 runnable packages in the `php-repos`:

- [Chuck Norris package](https://github.com/php-repos/chuck-norris)
- [Weather package](https://github.com/php-repos/weather)

The `chuck-norris` package will show a chuck norris joke in your terminal
and the `weather` package shows a beautiful weather forecast for your location.

For running these packages, you can simply call the `run` command:

```shell
phpkg run https://github.com/php-repos/chuck-norris // Shows a joke in your terminal
phpkg run https://github.com/php-repos/weather // Shows weather forecast on your terminal
```

> **Note**  
> For more information about `run`,
> please check [run documentation](https://phpkg.com/documentations/run-command).

### Use by serving an application

You can use `phpkg` to serve any phpkg package that has at least one entry point.
This feature allows you to serve an application and access it using a web browser.
For example, you can serve the [daily routine](https://github.com/php-repos/daily-routine) application by running:

```shell
phpkg serve https://github.com/php-repos/daily-routine.git
```

After running this command, you will see an output that indicated the application is ready to access on port 8000.

> **Note**
> For more information about `serve`,
> please check [serve documentation](https://phpkg.com/documentations/serve-command).

#### Migrate from composer

If you have a project that uses composer, and you wish to use `phpkg` on that project,
you can use the `migrate` command to make a config file that contains required namespace from your installed packages.

```shell
phpkg migrate
```

> **Note**  
> For more information about migrate command,
> please check [migrate documentation](https://phpkg.com/documentations/migrate-command).
