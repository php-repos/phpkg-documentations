## Introduction

When you decide to use Saeghe, you need to do some steps to prepare your application to take advantage of it.
You can do these steps by yourself, however, there is a faster way to do so, you can use `init` command in this case.

## Usage

Simply, run the following command on your application:

```shell
saeghe init
```

This command will create the required files and directories:
- It creates a `saeghe.config.json` file
- It creates a `saeghe.config-lock.json` file
- It creates a directory for storing packages source code in it, by default the name is `Packages`
- It created a `builds` directory for keeping builds files and directories 
([see build command documentation](https://saeghe.com/documentations/build-command))

As mentioned before, you can do all of these steps by yourself, however, 
running the command will be a much faster approach.

If you want to use other directories than `Packages` for keeping added packages, 
you can call the `init` command with `packages-directory` argument:

```shell
saeghe init --packages-directory=vendor
```

After having your application initialized, you may start to apply your configuration in the `saeghe.config.json` file.

See [customization documents](https://saeghe.com/documentations/customization)
