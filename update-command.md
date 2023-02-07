## Introduction

Packages may be updated over time, introducing newer versions.
When you need to update a package in your application,
you can use the `update` command to easily update to a specific version or the latest version.

## Usage

To update a package to its latest version, simply run the update command and pass the package's git URL:

```shell
phpkg update https://github.com/{owner}/{repo}.git
```

You can also specify a specific version to update to by passing the version tag to the update command:

```shell
phpkg update https://github.com/{owner}/{repo}.git --version={version-tag}
```

You may also define an alias for a package and use that alias to update the package:

```shell
phpkg alias my-package https://github.com/{owner}/{repo}.git
phpkg update my-package
```

> **Note**
> For more information about the `alias` command,
> please read [this documentation](https://phpkg.com/documentations/alias-command).

## Example

Assuming we have the `test-runner` package in our application, with the owner `php-repos` and repo name `test-runner`,
we can update it to the latest version with the following command:

```shell
phpkg update https://github.com/php-repos/test-runner.git
```

To update to a specific version, we can specify the version number:

```shell
phpkg update https://github.com/php-repos/test-runner.git --version=v1.0.1
```

If you defined an alias for the package, then you can use the alias for updating the package.
Let's assume we defined a `test-runner` alias for this package. Then you can run the following command:

```shell
phpkg update test-runner
```

For updating to a specific version:

```shell
phpkg update test-runner --version=v1.0.1
```
