## Introduction

You can use the `alias` command to register an alias for a specific package for your application.
The defined alias can be used on any other command that requires a package as an argument.

## Usage

For defining an alias, you need to pass an alias and its correspond package URL to the `alias` command:

```shell
saeghe alias datatype https://github.com:saeghe/datatype.git
```

After defining the alias, you can easily pass it to other commands:

```shell
saeghe add datatype
saeghe remove datatype
saeghe update datatype
```

Aliases must be unique in an application, but you are free to define as many alias that you need as aliases for a specific package:

```shell
saeghe alias test-runner https://github.com:saeghe/test-runner.git
saeghe alias tests https://github.com:saeghe/test-runner.git
saeghe alias saeghe/tests https://github.com:saeghe/test-runner.git
```
