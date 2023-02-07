## Introduction

You may already have an application or a package that uses Composer as the package manager.
If you wish to migrate, you can use the `migrate` command.

## Usage

On the package or application directory that you want to migrate, run the following command:

```shell
phpkg migrate
```

This command reads from your `composer.json` and `composer.lock` files 
and creates a `phpkg.config.json` file for your project.

After that, you can simply run the `build` command.

> **Note**  
> For migration you need to have your `vendor` directory installed from the composer.
