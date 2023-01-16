## Introduction

Before you can start using phpkg to manage your application's dependencies, you'll need to do some initial setup.
The `init` command can help you do this quickly and easily.

## Usage

To initialize your application for use with `phpkg`, simply run the following command in your project's root directory:

```shell
phpkg init
```

This command will create the following files and directories:

- A `phpkg.config.json` file, which contains the configuration settings for your application.
- A `phpkg.config-lock.json` file, which is used to keep track of the packages that have been added to your application.
- A directory for storing the source code of packages that you add to your application. By default, this directory is named `Packages`.

If you prefer to use a different directory name for storing added packages, you can specify it when you run the init command. 
For example:

```shell
phpkg init --packages-directory=vendor
```

Once your application has been initialized, you can start customizing your `phpkg.config.json` file to suit your needs.
For more information on how to do this, see the [customization documents](https://phpkg.com/documentations/customization).
