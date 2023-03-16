## Introduction

You can use the `serve` command to serve any `phpkg` package without installing it into any project.
Just pass the git URL for your desired package and start serving in your local.

> **Note**
> The package that you want to serve must have at least one entry point defined in its config file.

## Usage

You need to pass the package's git URL to the `serve` command. This command works with both, HTTPS and SSH git URL.

The `serve` command downloads, installs, builds, and serves the first entry point using `php -S` command.

```shell
phpkg serve https://github.com/{OWNER}/{REPO}.git [entry-point]
```

> **Note**
> If the given package has more than one entry point defined in its `phpkg.config.json` file, 
> then you need to pass a second argument to specify which entry point you need to run.
> Otherwise, it uses the first entry point defined in the config file.
> See [customization documents](https://phpkg.com/documentations/customization)

As an example, you can serve the `Daily Routine` package that shows a simple dashboard with various information to start your day, by running the following command:

```shell
phpkg serve https://github.com/php-repos/daily-routine.git
```

It's worth noting that the `serve` command will install the package in a temporary location, and it will be removed after restarting your OS.
Also, it will not add the package to your `phpkg.config.json` file, so it will not be available for future use in your application.
