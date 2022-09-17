## Introduction

As you know, we need to import used PHP files using one of [`require`](https://www.php.net/manual/en/function.require.php), 
[`include`](https://www.php.net/manual/en/function.include.php), 
[`require_once`](https://www.php.net/manual/en/function.require-once.php) and 
[`include_once`](https://www.php.net/manual/en/function.include-once.php) expressions.
This is a frustrating job to keep all imports in sync with file and directory changes.

This is the place that Saeghe comes to solve for you. You can write your PHP code, without considering file locations. 
Then Saeghe will resolve and add them for you, either they are on your application or they come from another package.

## Usage

By running the following command, you can build your application for the `development` environment:

```shell
saeghe --command=build
```

After running this command, you will have a clone of your application under `builds/development` directory.
When you run the build command, Saeghe uses your `saeghe.config.json` file and builds your application based on defined configs on this file.

> **Note**  
> Please read [configuration documentation](https://saeghe.com/documentations/customization) to customize you’re builds.

You can also build your application for the production environment like so:

```shell
saeghe --command=build --environment=production
```

By running this command, you will see a built copy of your application in `builds/production` directory.

> **Note**  
> Currently, except build environment directory, there is no difference between `development` and `production` build. 
> But soon there will come many cool features and boosts for your production code.
