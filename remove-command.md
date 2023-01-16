## Introduction

It is a common use case that you sometimes need to remove an added package from your application.
The `remove` command allows you to easily remove a package from your application.

## Usage

The `remove` command takes the package's name or URL as an argument. 
You can pass the ssh or https URL of the package to the `remove` command.

```shell
// Remove using a https URL
phpkg remove https://github.com/{owner}/{repo}
// Remove using a ssh URL
phpkg remove git@github.com:{owner}/{repo}.git
```

Alternatively, you can define an alias for a specific package using the `alias` command and then use the defined alias for removing the package.

```shell
phpkg alias package-alias git@github.com:{owner}/{repo}.git
phpkg remove package-alias
```

> **Note**
> For more information about the `alias` command,
> please read [this documentation](http://phpkg.com/documentations/alias-command).
 
When you run the `remove` command, the given package will be removed from your package's directory, `phpkg.config.json` file, and `phpkg.config-lock.json` file.

> **Note**  
> If you are not sure what path you used to add the package, you can always check the packages section in your `phpkg.config.json` file to see the path.

## Examples

Let's assume we added the `test-runner` package from `php-repos/test-runner`. 
To remove the package from your application, you can run the following command:

```shell
phpkg remove https://github.com/php-repos/test-runner
```

Using an alias for the package can make it easier:

```shell
phpkg alias test-runner https://github.com/php-repos/test-runner
phpkg remove test-runner
```
