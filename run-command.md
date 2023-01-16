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

It's worth noting that the `run` command will install the package in a temporary location and it will be removed after running.
Also, it will not add the package to your `phpkg.config.json` file, so it will not be available for future use in your application.
