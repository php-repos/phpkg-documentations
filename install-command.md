## Introduction

Most probably, you are not going to commit your packages directory into your git repo.
This is one of the reasons you want to use a package manager.
So now, when you want to work on the same project on another machine,
or when you want to deploy your application,
you need to download same repositories and install the required packages.
As you can guess, there is a simple command that you need to run to install all your packages.

## Usage

To install all used packages in your application and their packages that are saved in your `saeghe.config-lock.json` file, run:

```shell
saeghe install
```

And you will see the same copy of the used packages in the packages' directory.
