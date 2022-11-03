## Introduction

Currently, there are two options for installing Saeghe.
Both of these methods are going to install it in your home directory,
so you can get access to it from any path and use it as all your projects’ package managers.

> **Note**  
> These installations work on Unix/Linux and macOS systems.
> Support for windows will be added soon.

## Requirements

You need to have git installed on your machine as well as PHP version >= 8.0
with `php-mbstring`, `php-zip`, and `php-curl` extensions installed.

## Step 1: Download

First step is to download required files. You can do it automatically or manually.

### Use Installer

Using the installer will be the easiest method.
You can simply run the following line, and you should have it ready to use:

```shell
bash -c "$(curl -fsSL https://raw.github.com/saeghe/installation/master/install.sh)"
```

This command is going to make a `.saeghe` directory in your home directory and,
it installs the required source files under this directory.
It also adds its source directory to your `$PATH` so you can easily start to use it.

### Manual Installation

You can manually install it by following these steps:

- Download the latest version from [github](https://github.com/saeghe/saeghe/releases)
- Unzip the downloaded file
- Rename the unzipped directory to `saeghe`
- Download the latest version of `cli` package from [github](https://github.com/saeghe/cli/releases)
- Unzip the cli package and move its files and directories to `saeghe/Packages/saeghe/cli`
- Make a copy from `credentials.example.json` to `.credentials.json`
- Add path to its source directory into your `$PATH`
- To make sure everything is installed correctly, run `saeghe --help` and you should see the help.

## Step 2: Source your terminal

If you used the installer, a path to the Saeghe has been added to your source file (`.bashrc` or `.zshrc`). 
You need to either, open a new terminal or source your current terminal to get access to new added path.

## Step 3: Add GitHub token

You need to have a GitHub access token. A GitHub token is required to read repositories.
You can generate a token by following this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
Then you can use the following command to add it to credentials:

```shell
saeghe credential github.com {your-github-token}
```
