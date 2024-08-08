## Introduction

You can use the `run` command to run any `phpkg` package without installing it into any project.
Just pass the git URL for your desired package and see the output on the console.

## Usage

You need to pass the package's git URL to the `run` command. This command works with both, HTTPS and SSH git URL.

The `run` command downloads, installs, builds, and runs the given package's entry point.

```shell
phpkg run https://github.com/{OWNER}/{REPO}.git [entry-point]
```

> **Note**
> If the given package has more than one entry point defined in its `phpkg.config.json` file, 
> then you need to pass a second argument to specify which entry point you need to run.
> Otherwise, it uses the first entry point defined in the config file.
> See [customization documents](https://phpkg.com/documentations/customization)

As an example, you can run the `Chuck Norris` package that sends a request to the https://api.chucknorris.io/ and shows the
result on the output by running the following command:

```shell
phpkg run https://github.com/php-repos/chuck-norris.git
```

You can also see your location's weather forecast in your terminal by running the following command:

```shell
phpkg run https://github.com/php-repos/weather.git
```

It's worth noting that the `run` command will install the package in a temporary location, and it will be removed after restarting your OS.
Also, it will not add the package to your `phpkg.config.json` file, so it will not be available for future use in your application.

You may wish to `run` a package on a specific version. For doing so, pass a `version` arg indicating your desired version:

```shell
phpkg run https://github.com/owner/repo.git --version={version}
```

If you came across a need to run a package on a specific commit hash, you can use the `version` argument using `development#{commit-hash}`:

```shell
phpkg run https://github.com/php-repos/chuck-norris.git --version=development#336212f42b0d612a1397e5009f2e3c681851d770
```

While developing, you might need to `run` another package that is already on your machine. In this case, you can use either a relative or an absolute path to the project from your current directory, rather than the package's URL:

```shell
phpkg run ../relative/path/to/packge
phpkg run ./absolute/path/to/package
```
