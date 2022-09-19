## Introduction

Currently, there are two options for installing Saeghe. 
Both of these methods are going to install Saeghe to your home directory, 
so you can get access to Saeghe from any path and use it as all your project's package manager.

> **Note**  
> These installations work on Unix/Linux and MacOS systems. 
> Support for windows will be added soon.

## Use Installer

Using the installer will be the easiest method to install Saeghe. 
You can simply run the following line, and you should have it ready to use:

```shell
sh -c "$(curl -fsSL https://raw.github.com/saeghe/installation/master/install.sh)"
```

This command is going to make a `.saeghe` directory in your home directory and,
it installs required source files under this directory. 
It also adds Saeghe's source directory to your `$PATH` so you can easily start to use it.

## Manual Installation

You can manually install Saeghe by following these steps:

- Download the latest version of Saeghe from [github](https://github.com/saeghe/saeghe/releases)
- Unzip the downloaded file
- Rename the unzipped directory to `saeghe`
- Download the latest version of `cli` package from [github](https://github.com/saeghe/cli/releases)
- Unzip the cli package and move its files and directories to `saeghe/Packages/saeghe/cli`
- Make a copy from `credentials.example.json` to `.credentials.json`
- Add path to Saeghe source directory into your `$PATH`
- To make sure everything is installed correctly, run `saeghe --help` and you should see the help.
