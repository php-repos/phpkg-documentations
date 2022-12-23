## Introduction

Packages will improve over time, so they introduce newer versions. 
Now, if you used an old version, you need to update the package to use a newer version,
a specific version or the latest version.

## Usage

For updating a package to its latest package, simply, run the update command and pass the package's path:

```shell
saeghe update https://github.com/{owner}/{repo}.git
```

Sometimes, you may need to update a package to a specific version. 
In this case, you need to just pass the version tag to the update command:

```shell
saeghe update https://github.com/{owner}/{repo}.git --version={version-tag}
```

It removes the current version of the package from your application 
and then adds the latest version of your desired version.

You may define an alias for the package therefore, later you can use the defined alias for updating the package:

> **Note**
> For more information about the `alias` command,
> please read [this documentation](http://saeghe.com/documentations/alias-command).

## Example

Let's assume we have the `test-runner` package in our application. 
This package's owner is `saeghe` and the repo name is `test-runner`. 

```shell
saeghe update https://github.com/saeghe/test-runner.git
```

Running this command will remove the current version of the package 
and adds the latest available version for the `test-runner` package.

If we need to have a specific version of the `test-runner`, 
then you need to specify the version number:

```shell
saeghe update https://github.com/saeghe/test-runner.git --version=v1.0.1
```

If you defined an alias for the package, then you can use the alias for updating the package.
Let's assume we defined a `test-runner` alias for this package. Then you can run the following command:

```shell
saeghe update test-runner
```

For updating to a specific version:

```shell
saeghe update test-runner --version=v1.0.1
```
