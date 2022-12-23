## Introduction

It is a common use case that you sometimes need to remove an added package from your application.
Removing a package from your application is also a very easy process.

## Usage

The only thing you need to pass is the package’s path.

You can pass the ssh URL or the https URl of the package to the remove command.

```shell
// Remove using a https URL
saeghe remove https://github.com/{owner}/{repo}
// Remove using a ssh URL
saeghe remove git@github.com:{owner}/{repo}.git
```

Alternatively you might define an alias for a specific package and then use the defined alias for removing the package.

```shell
saeghe alias package-alias git@github.com:{owner}/{repo}.git
saeghe remove package-alias
```

> **Note**
> For more information about the `alias` command,
> please read [this documentation](http://saeghe.com/documentations/alias-command).

The given package will be removed from your package’s directory, `saeghe.config.json` file, and `saeghe.config-lock.json` file.

> **Note**  
> If you are not sure what path did you use for adding the package,
> you can always check the `packages` section in your `saeghe.config.json` file to see the path.

## Example

let's assume we added the `test-runner` package from `saeghe/test-runner`,
now for removing the package from your application, you can run the following command:

```shell
saeghe remove https://github.com/saeghe/test-runner
```

Using an alias for the package can make it easier:

```shell
saeghe alias test-runner https://github.com/saeghe/test-runner
saeghe remove test-runner
```

