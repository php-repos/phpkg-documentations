## Introduction
The [init command](https://phpkg.com/documentations/init-command) in phpkg creates a `phpkg.config.json` file for your application,
where you can find all configurable options.
This file contains various sections that allow you to customize the behavior of `phpkg` to suit your needs.

## What is included in the config file?

After running the `init` command, you will find a `phpkg.config.json` file with the following sections:

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
Let's take a closer look at each of these sections:

### Map

This section allows you to map namespaces to specific directories in your application. 
For example, if you want to map the `MyAwesomeApplication` namespace to the `src directory,
you would add the following configuration:

```json
{
  "map": {
    "MyAwesomeApplication": "src"
  }
}
```

You can also map other namespaces, such as `Tests` to the `tests` directory:

```json
{
  "map": {
    "MyAwesomeApplication": "src",
    "Tests": "tests"
  }
}
```

You can add as many mappings as you need, and `phpkg` will ensure they are properly resolved in your application.

### Entry Points

This config should point to your entry points files.
For example, let's assume you have 2 entry points, one for HTTP requests and one for CLI requests.
For HTTP requests, the file is in `{PROJECT_ROOT_DIRECTORY}/public/index.php`
and for CLI, the entry file is `{PROJECT_ROOT_DIRECTORY}/cli-runner.php`.
in this case, you need to define entry points as follows:

This section allows you to specify the entry points of your application.
For example, if you have separate entry points for HTTP requests and CLI requests like:

- `{PROJECT_ROOT_DIRECTORY}/public/index.php` for HTTP requests
- `{PROJECT_ROOT_DIRECTORY}/cli-runner.php` for CLI

you would add the following configuration:

```json
{
  "entry-points": [
    "public/index.php",
    "cli-runner.php"
  ]
}
```

`phpkg` will automatically add the required autoloading using class maps for classes in these entry point files.

### Excludes

Normally, all files and directories in your application are included in the build process.
However, there may be certain files or directories that you don't want to include in your built application.
For example, you may have a `node_modules` directory or a bash file like `make.sh` that you don't need in your project runtime.
The excludes config allows you to specify files or directories that should be ignored during the build process.

To exclude a file or directory, simply add it to the excludes array in your `phpkg.config.json` file:

```json
{
  "excludes": [
    "node_modules",
    "make.sh"
  ]
}
```

This config is useful for keeping your built application lean and reducing the number of unnecessary files.
It's also useful for removing files or directories that may cause issues in production environments,
such as sensitive files or development dependencies.

Also, it's important to note that the excludes config is relative to the project's root directory.

### Executables

If you are developing a package, or you want to separate your main application into smaller packages,
you may end up having some executable files that you want to have in your main application as well.
For example, let's assume you are developing a package named `rocket` and it contains an executable file named `launch.php`.
You can define this file as an executable in your main application by adding the following to your `phpkg.config.json`:

```json
{
  "executables": {
    "rocket-launch": "vendor/rocket/launch.php"
  }
}
```

This configuration will create a symlink in the root of your application named `rocket-launch` that points to the `launch.php` file inside the `vendor/rocket` directory.

It's important to note that the path to the executable file should be relative to the root of your application,
and that the executable will have the same dependencies and class maps as the package it belongs to.

Additionally, you can also specify multiple executables in the same configuration like so:

```json
{
  "executables": {
    "rocket-launch": "vendor/rocket/launch.php",
    "rocket-status": "vendor/rocket/status.php"
  }
}
```

This will create two executables in the root of your application,
one named `rocket-launch` and the other named `rocket-status`,
that point to the `launch.php` and `status.php` files respectively inside the `vendor/rocket` directory.

### Packages Directory

The `packages-directory` config sets the default directory for adding and removing packages to your application,
as well as the default package directory for building your application's packages.
By default, `phpkg` uses the directory `Packages` for package management, but you can customize it to any directory name you prefer.

For example, if you want to use the directory vendor for package management, you can set the config as follows:

```json
{
  "packages-directory": "vendor"
}
```

With this configuration, when you add or remove a package using `phpkg`,
it will look for or create the package in the `vendor` directory.
Also, when you build your application, the packages will be placed in the `vendor` directory.

It's important to note that if you change the `packages-directory` config,
you need to make sure that the new directory is included in your project's `.gitignore` 
or `.ignore` file to prevent unwanted files from being committed to the repository.

> **Note**  
> If the specified directory does not exist, phpkg will create it for you.

### Packages

The `packages` config is used to keep track of the packages that are installed in your application.
It is automatically populated by `phpkg` when you use the `add`, `update`, or `remove` commands.
The config lists the package name, version, and repository URL for each package that is installed.

Here is an example of what the `packages` config might look like:

```json
{
  "packages": {
    "https://github.com/php-repos/test-runner.git": "1.0.0",
    "https://github.com/php-repos/datatype.git": "2.5.0"
  }
}
```

This configuration keeps track of the packages that have been added to your application,
and their version and URL, so that phpkg can check for `updates`, `remove`, or `build` your application with the correct versions.
