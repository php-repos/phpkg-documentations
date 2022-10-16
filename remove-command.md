## Introduction

It is a common use case that you sometimes need to remove an added package from your application.
Removing a package from your application using Saeghe is also a very easy process.

## Usage

The only thing you need to pass is the package’s path.

If you added the package using the HTTPS URL then simply replace the owner and the repo name in the following command and run it:

```shell
saeghe remove https://github.com/{owner}/{repo}
```

If you used the SSH path for adding the package you need to run:

```shell
saeghe remove git@github.com:{owner}/{repo}.git
```

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

