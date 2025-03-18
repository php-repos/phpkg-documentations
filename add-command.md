## Add Command

### Bring Git Packages into Your Project

Need a package in your `phpkg` project? The `add` command grabs any Git repo—public or private—and drops it into your setup, ready to autoload functions and classes. No central registry, no fuss—just find a repo and add it.

- **For Users**: Search GitHub, copy the URL, and go.
- **For Devs**: Push your code to Git—it’s instantly usable, no extra steps.

---

### Usage

Add a package with its Git URL:

```bash
phpkg add <package-url>
```

- **HTTPS**:  
    ```bash
    phpkg add https://github.com/owner/repo.git
    ```
- **SSH**:
    ```bash
    phpkg add git@github.com:owner/repo.git
    ```

Replace `owner` and `repo` with the real deal—e.g., `php-repos/test-runner`.

#### Use an Alias

Set a shortcut with [Alias Command](https://phpkg.com/documentations/alias-command) first:
```bash
phpkg alias tr https://github.com/php-repos/test-runner.git
phpkg add tr
```

#### Pick a Version

By default, `phpkg` grabs the latest release:
```bash
phpkg add https://github.com/php-repos/test-runner.git
```

- Want a specific tag? Add `--version`:  
    ```bash
    phpkg add https://github.com/php-repos/test-runner.git --version=v1.2.3
    ```
- Semantic versioning? Use a prefix:  
    ```bash
    phpkg add https://github.com/php-repos/test-runner.git v1  # Latest v1.x.x
    ```
- Need the dev version? Go with:  
    ```bash
    phpkg add https://github.com/php-repos/test-runner.git --version=development
    ```
    Clones the repo if no releases exist.

#### GitHub Token Note

Busy project or private repo? `phpkg` needs a GitHub token to avoid rate limits or access locked code. Set `GITHUB_TOKEN` env var or use [Credential Command](https://phpkg.com/documentations/credential-command):

```bash
phpkg credential github.com <your-token>
```

---

#### What Happens?

- **Package Location**: Lands in `Packages/owner/repo` (or your custom `packages-directory`).  
- **Config Update**: Adds to `phpkg.config.json`:  
    ```json
    {
        "packages": {
            "https://github.com/php-repos/test-runner.git": "v1.2.3"
        }
    }
    ```
- **Lock File**: Tracks metadata in `phpkg.config-lock.json`:  
    ```json
    {
        "https://github.com/php-repos/test-runner.git": {
            "version": "v1.2.3",
            "hash": "abc123...",
            "owner": "php-repos",
            "repo": "test-runner"
        }
    }
    ```
- **Next**: Run `phpkg build` to autoload its functions and classes.

---

#### Example

Add the `test-runner` package:
```bash
phpkg add https://github.com/php-repos/test-runner.git
```

- Installs to `Packages/php-repos/test-runner`.  
- Updates configs with the latest release (or dev if no releases).

Try a Composer package too:

```bash
phpkg add https://github.com/symfony/thanks.git
```

`phpkg` handles any Git repo—Composer or not.

---

### Tips

- **Rate Limits**: Lots of packages or releases? Add a token to keep it smooth.  
- **Versions**: Check repo tags online—`phpkg` picks what’s there.  
- **Next Steps**: See [Build Command](https://phpkg.com/documentations/build-command) to use your new package.
