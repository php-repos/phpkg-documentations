## Introduction

f your project needs to use external packages, `phpkg` needs to access repositories on GitHub. 
In order to do so, it requires an access token. 
You can use the `credential` command to add your token.

> **Note**
> If you already have an environment variable named `GITHUB_TOKEN` with your GitHub token, then you don't need to do anything.

## Usage

First, follow this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 
and generate an access token. Then run the following command:

```shell
phpkg credential github.com {your-github-access-token}
```

This will allow phpkg to access the GitHub APIs and read repositories.
