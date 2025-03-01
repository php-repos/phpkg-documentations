## Introduction

Currently, there are two options for installing `phpkg`.
Both of these methods are going to install it in your home directory,
so you can get access to it from any path and use it as all your projects’ package managers.

## Requirements

You need to have `unzip` and `git` installed on your machine as well as PHP version >= 8.1 
with `php-mbstring`, `php-zip`, and `php-curl` extensions installed.

## Installation

### Step 1: Run the installer

> **Note**  
> These installer work on Unix/Linux and macOS systems. Support for windows will be added soon.

Installing phpkg using the installer is very easy.
You can simply run the following line, and you should have it ready to use:

```shell
bash -c "$(curl -fsSL https://raw.github.com/php-repos/phpkg-installation/master/install.sh)"
```

This command will make a `.phpkg` directory in your home directory and,
it installs the required source files under this directory.
It also adds its source directory to your `$PATH` so you can easily start to use it.

You need to open a new terminal to be able to use commands on `phpkg`.

### Step 2: Source your terminal

When you use the installer, a path to phpkg is added to your shell configuration file (either `.bashrc` or `.zshrc`).
To access the newly added path, you need to either open a new terminal or source your current terminal session.