## Introduction

You can use the `alias` command to register an alias for a specific package for your application. 
The defined alias can be used on any other command that requires a package as an argument.
This feature can be useful when you want to use a package in multiple places in your application,
and you don't want to remember the full package url.

## Usage

For defining an alias, you need to pass an alias and its correspond package URL to the `alias` command:

```shell
phpkg alias your-alias https://github.com:{owne}/{repo}
```

For example:

```shell
phpkg alias datatype https://github.com:php-repos/datatype.git
```

After defining the alias, you can easily pass it to other commands:

```shell
phpkg add datatype
phpkg remove datatype
phpkg update datatype
```

Aliases must be unique in an application, but you are free to define as many alias that you need as aliases for a specific package:

```shell
phpkg alias test-runner https://github.com:php-repos/test-runner.git
phpkg alias tests https://github.com:php-repos/test-runner.git
phpkg alias php-repos/tests https://github.com:php-repos/test-runner.git
```
