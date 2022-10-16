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
> **Note**  
> If you are not sure what path did you use for adding the package, 
> you can always check the `packages` section in your `saeghe.config.json` file to see the path.

Saeghe will remove the current version of the package from your application 
and then adds the latest version of your desired version.

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
