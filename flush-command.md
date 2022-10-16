## Introduction

When you run the build command on Saeghe, 
it creates an "environment build" directory inside the `builds` directory 
and then builds all files and moves them inside this directory.

You may wish to clear these directories entirely. You can use the `flush` command in this case.

## Usage

Inside your application, run this command:

```shell
saeghe flush
```

Now if you check the environment build directory 
([check build documentation](https://saeghe.com/documentations/build-command)) 
you should not see any file under this directory.
