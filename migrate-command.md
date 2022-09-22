## Introduction

You may already have an application or a package that uses composer as the package manager.
If you wish to use Saeghe for this case, you can use the `migrate` command.

## Usage

On the package or application directory that you want to migrate, run the following command:

```shell
saeghe migrate
```

This command reads from your `composer.json` and `composer.lock` files and migrates your used packages
from the `vendor` directory to a `Packages` directory. It also makes `saeghe.config.json` and
`saeghe.config-lock.json` files for your application/package and all dependencies.

After that, you can simply run `build` command.

> **Note**  
> For migration you need to have your `vendor` directory installed from the composer.

> **Note**  
> The `migrate` command will not guarantee to migrate everything properly yet.
> There might be required for you to add some `use` statements in used classes.
