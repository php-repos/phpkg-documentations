## Introduction

If your project needs to use external packages, Saeghe will need to read repositories from Github. 
It needs to have an access token to read repositories. 
You can use the `credentail` command to add your token.

## Usage

First, follow this [link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 
and generate an access token. Then run the following command:

```shell
saeghe credential github.com {your-github-access-token}
```

That's it. Now Saeghe can get access to GitHub APIs.
