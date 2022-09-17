## Introduction

Most probably, you are not going to commit your packages directory into your git repo. 
This is one of the reason you probably want to use a package manager.
So now, you want to download your repo and install required packages.
As you can guess, there is a simple command that you need to run to install all your packages.

## Usage

Saeghe will use your `saeghe.config-lock.json` file, to install all used packages in your application and their packages. Run:

```shell
saeghe --command=install
```

And you will see the same copy of the used packages in your packages directory.
