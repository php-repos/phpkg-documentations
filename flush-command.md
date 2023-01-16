## Introduction

The `flush` command is used to remove all the files and directories that were created during the build process.
This command can be useful when you want to start a fresh build or when you want to clear any unnecessary files 
that may have been created during the build process.

## Usage

To use the `flush` command, navigate to the root directory of your application and run the following command:

```shell
phpkg flush
```

This command will remove all the files and directories that were created in the "environment build" directory inside the `builds` directory.

> **Note**  
> Be careful when using this command, as it will delete all the files and directories that were created by the build command.
> Make sure to backup any necessary files before running this command.

After running this command, you can check the "environment build" directory to confirm that it is empty.
You can then run the `build` command again to start a fresh build of your application.
