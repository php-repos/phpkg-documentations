## Introduction

Once you've added all the required packages to your application using the `add` command,
you may want to install them on another machine or environment.

The `install` command allows you to install all of the packages defined in your `phpkg.config.json` file.
It uses the `packages` config section to determine which packages should be installed.

## Usage

To install all of the packages defined in your `phpkg.config.json` file, simply run the following command in your application:

```shell
phpkg install
```

This command will install all of the packages defined in your `phpkg.config.json` file's packages config section
and will place them in the directory defined in the `packages-directory` config section.
If the directory does not exist, it will be created.

> **Note**
> Make sure that you've run the `add` command before running the `install` command
> to ensure that all of the required packages are defined in your `phpkg.config.json` file.
> Please see [add command documentation](https://phpkg.com/documentations/add-command)

