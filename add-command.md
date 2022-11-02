## Introduction

You can use the `add` command to add a git repository to your application as a package.

As a package user, simply search online, and as soon as you reach the git repo, you can add it.

As a package developer, there is no need to register your package in other places.
Your package is ready to use as soon as you push it to the git.

## Usage

Adding a package to your application using the `add` command is very easy.
You only need to provide a path to your desired package, and it adds that package to your application.

The path can be an HTTPS path or SSH path to the package.

For HTTPS path use:

```shell
saeghe add https://github.com/{owner}/{repo}.git
```

For SSH path use:

```shell
saeghe add git@github.com:{owner}/{repo}.git
```

You can simply add any package to your application using this single command.
Remember to replace `{owner}` and `{repo}` with your desired package owner and repo name.

By default, it checks the given package's repository to see if there are any releases for the package.
If it finds releases, it downloads the latest release of the package for your application,
unless you specify the version tag that you wish to install.

```shell
saeghe add https://github.com/{owner}/{repo}.git --version={tag-name}
```

In this case, it adds the same version of the package to your application.

However, sometimes you may need a development version of a package.
In this case, you can specify `development` as the version tag, and it clones the package for your application.
Cloning the package also happens when there is no release for the package.

> **Note**  
> If you are adding a private package, you will need a token for cloning or downloading the package.
> You must add your access token in the `.credential` file under the saeghe installation directory.
>
> For more information about generating the personal access token,
> please read [this documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Example

Let's say you need to install the `test-runner` package to our application.
The owner of this package is `saeghe` and the repo is `test-runner`.
You only need to run:

```shell
saeghe add https://github.com/saeghe/test-runner
```
And it will install the package to `Packages/saeghe/test-runner` on your project directory.

You will see the package in your `saeghe.config.json` file under the `packages` section:

```json
"packages": {
    "git@github.com:saeghe\/test-runner.git": "version-number"
}
```

The package metadata will be added to the `saeghe.config-lock.json` file:

```json
"git@github.com:saeghe\/test-runner.git": {
    "version": "version-number",
    "hash": "hash-for-installed-version",
    "owner": "saeghe",
    "repo": "test-runner"
}
```

