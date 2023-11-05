## Introduction

The [init command](https://phpkg.com/documentations/init-command) in phpkg is a powerful tool that generates a `phpkg.config.json` file for your application. This configuration file serves as the control center for customizing various aspects of `phpkg` to align with your specific requirements.

## What is Included in the Configuration File?

Upon executing the `init` command, you will discover a `phpkg.config.json` file that contains the following key sections:

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

Let's delve into each of these sections individually:

### Map

This section empowers you to map namespaces to specific directories within your application. For example, if you wish to map the `MyAwesomeApplication` namespace to the `src` directory, you can include the following configuration:

```json
{
  "map": {
    "MyAwesomeApplication": "src"
  }
}
```

You can also map additional namespaces, such as `Tests`, to the `tests` directory:

```json
{
  "map": {
    "MyAwesomeApplication": "src",
    "Tests": "tests"
  }
}
```

Feel free to add as many mappings as needed, and `phpkg` will ensure their proper resolution within your application. It's essential to adhere to `PSR-4` standards when defining your classes and functions, and `phpkg` will handle imports using your specified mapping.

As an example, if you've defined a class in your mapping, such as a `User` class, you should create a `User.php` file under the `src` directory. Here's how you can structure the `src/User.php` file:

```php
<?php

namespace MyAwesomeApplication;

class User
{
    // Your class code here
}
```

For functions within a specific namespace, suppose you want to create a `Service` namespace for defining functions. In that case, you should add a `Service.php` file under the `src` directory, like this:

```php
<?php

namespace MyAwesomeApplication\Service;

function service_a()
{
    // Your function code here
}
```

### Autoloads

This section enables you to specify a list of files that should be autoloaded before any other code execution. For instance, if you have a `Helper.php` file containing a set of functions that you want to load during the autoload process, you can configure it as follows:

```json
{
  "autoloads": [
    "helper.php"
  ]
}
```

The `autoloads` section is an array, allowing you to define multiple files for autoload.

### Excludes

While the default behavior includes all files and directories in your application during the build process, there may be specific files or directories you wish to exclude. This is especially relevant for files or directories that serve no purpose in your project's runtime, such as `node_modules` or development scripts like `make.sh`. The `excludes` configuration empowers you to specify files or directories that should be disregarded during the build process.

To exclude a file or directory, simply add it to the `excludes` array in your `phpkg.config.json` file:

```json
{
  "excludes": [
    "node_modules",
    "make.sh"
  ]
}
```

The `excludes` configuration is defined relative to the root directory of your project.

### Entry Points

This section allows you to define the entry points of your application. For example, if your application has distinct entry points for HTTP requests and CLI requests, you can specify them as follows:

```json
{
  "entry-points": [
    "public/index.php",
    "cli-runner.php"
  ]
}
```

`phpkg` will automatically facilitate the necessary autoloading using class maps for classes in these entry point files.

### Executables

If you are developing a package or wish to separate your main application into smaller packages, you may have executable files that you want to include in your main application. For example, if you are developing a package named `rocket` containing an executable file called `launch.php`, you can include this file in your main application by adding the following to your `phpkg.config.json`:

```json
{
  "executables": {
    "rocket-launch": "vendor/rocket/launch.php"
  }
}
```

This configuration will create a symlink in the root of your application named `rocket-launch`, which points to the `launch.php` file within the `vendor/rocket` directory. It's important to note that the path to the executable file should be relative to your application's root, and the executable will inherit the dependencies and class maps of the package it belongs to.

Furthermore, you can specify multiple executables within the same configuration, like so:

```json
{
  "executables": {
    "rocket-launch": "vendor/rocket/launch.php",
    "rocket-status": "vendor/rocket/status.php"
  }
}
```

This will create two executables in the root of your application, one named `rocket-launch` and the other named `rocket-status`, pointing to the `launch.php` and `status.php` files, respectively, inside the `vendor/rocket` directory.

### Import File

By default, `phpkg` generates a `phpkg.imports.php` file and adds the required import statements to that file, which is later imported in your entry points. However, this section allows you to customize the import file and use a path that better suits your project. For instance, if you prefer to use `vendor/autoload.php`, you can define the following configuration:

```json
{
  "import-file": "vendor/autoload.php"
}
```

### Packages Directory

The `packages-directory` configuration sets the default directory for adding and removing packages from your application, as well as the default package directory for building your application's packages. By default, `phpkg` uses the `Packages` directory for package management, but you can customize it to your preferred directory name.

For example, if you want to use the directory `vendor` for package management, you can configure it as follows:

```json
{
  "packages-directory": "vendor"
}
```

With this configuration, when you add or remove a package using `phpkg`, it will seek or create the package in the `vendor` directory. Additionally, when you build your application, the packages will be placed in the `vendor` directory.

It's crucial to note that if you modify the `packages-directory` configuration, you should ensure that the new directory is included in your project's `.gitignore` or `.ignore` file to prevent unintended files from being committed to the repository.

> **Note**  
> If the specified directory does not exist, `phpkg` will create it for you.

### Packages

The `packages` configuration is used to maintain a record of the packages installed in your application. This information is automatically populated by `phpkg` when you use the `add`, `update`, or `remove` commands. The configuration lists the package name, version, and repository URL for each installed package, ensuring that

`phpkg` can accurately perform tasks such as updates, removals, and building your application with the correct versions.

Here is an example of what the `packages` configuration might resemble:

```json
{
  "packages": {
    "https://github.com/php-repos/test-runner.git": "1.0.0",
    "https://github.com/php-repos/datatype.git": "2.5.0"
  }
}
```

This configuration maintains a record of the packages added to your application, along with their versions and repository URLs, streamlining the management of your application's dependencies.
