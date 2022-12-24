## Introduction

You can use the `run` command to run any Saeghe package without installing it into any project.
Just pass the git URl for your desired package and see the output on the console.

## Usage

You need to pass the package's git URL to the `run` command. This command works with both, HTTPS and SSH git URL.

The `run` command downloads, installs, builds and runs the given package's entry point.

> **Note**
> If the given package has more than one entry point defined in its `saeghe.config.json` file, 
> then you need to pass a second argument to specify which entry point you need to run.
> See [customization documents](https://saeghe.com/documentations/customization)

As an example, we created a Chuck Norris package that sends a request to the `https://api.chucknorris.io/` and shows the 
result on the output.

You can run it by the following command:

```shell
saeghe run https://github.com/saeghe/chuck-norris.git
```

By running this command, you will see the output in your terminal.

You can see your location's weather forecast in your terminal by running the following command:

```shell
saeghe run https://github.com/saeghe/weather.git
```
