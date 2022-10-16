## Introduction

As part of the [init command](https://saeghe.com/documentations/init-command),
Saeghe will create a `saeghe.config.json` file for your application.
You can find any configurable option on that file here.

## What is included?

After running the `init` command, you should see a `saeghe.config.json` file with the following content:

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
Let's dive into each of them separately.

### Config map

In this config, you can add your desired map for namespaces.
For example, assume you want to map the `MyAwesomeApplication` namespace to point to the `src` directory.
Then you should define:

```json
{
  "map": {
    "MyAwesomeApplication": "src"
  }
}
```

Now assume you put your tests in the `tests` directory and
you want to use the `Tests` namespace to point to the `tests` directory. Then you will have:

```json
{
  "map": {
    "MyAwesomeApplication": "src",
    "Tests": "tests"
  }
}
```

You can have as many as you need to map and Saeghe will make sure to resolve all of them in your application.

### Config entry-points

This config should point to your entry points files.
For example, let's assume you have 2 entry points, one for HTTP requests and one for CLI requests.
For HTTP requests, the file is in `{PROJECT_ROOT_DIRECTORY}/public/index.php`
and for CLI, the entry file is `{PROJECT_ROOT_DIRECTORY}/cli-runner.php`.
in this case, you need to define entry points as follows:

```json
{
  "entry-points": [
    "public/index.php",
    "cli-runner.php"
  ]
}
```

Saeghe will add require maps for autoloading objects in these files.

### Config excludes

Normally, Saeghe will try to build all files in all directories in your application.
Sometimes you don't need to have some files or directories in your build directory.
For example, let's say your application contains a `node_modules` directory
and a bash file like `make.sh` that you don't need in your project runtime.
Now you can add these two items into the `excludes` parameter and Saeghe will ignore them
and you won't see them in the final built directory.
You need to add the following:

```json
{
  "excludes": [
    "node_modules",
    "make.sh"
  ]
}
```

### Config executables

If you are developing a package, or you want to separate your main application into smaller packages,
you may end up having some executable files that you want to have in your main application as well.
For example, let's assume you are developing a package named `rocket`
add this package has an executable file named `check-runner.php`.
Now if you want to see the file as an executable file in the main application,
you need to have the following configuration:

```json
{
  "executables": {
    "rocket-check-runner": "check-runner.php"
  }
}
```
Having this configuration ends up seeing a `rocket-check-runner` file from the main application
linked to the `check-runner.php` file inside the package directory.
Saeghe automatically will add the required code for autoloading used classes to your executables files.

### Config packages-directory

This config sets the default directory for adding/removing packages to your application,
as well as the default package directory for building your application's package.
You can simply use any directory name for this config:

```json
{
  "packages-directory": "vendor"
}
```

### Config packages

You don't have to do anything with this config.
Saeghe will use this config to keep track of the required packages for your application.

