# Add Command

## Bring Git Packages into Your Project

Need a package in your `phpkg` project? The `add` command grabs any Git repo—public or private—and drops it into your setup, ready to autoload functions and classes. No central registry, no fuss—just find a repo and add it.

- **For Users**: Search GitHub, copy the URL, and go.
- **For Devs**: Push your code to Git—it's instantly usable, no extra steps.

---

## Usage

Add a package using a simplified format or full Git URL:

```bash
phpkg add <package-identifier>
```

### Simplified Formats

For GitHub packages, you can use the `owner/repo` format:
```bash
phpkg add php-repos/observer
phpkg add owner/repo
```

For packages in the `php-repos` organization, you can use just the repo name:
```bash
phpkg add observer
phpkg add datatype
```

### Full Git URLs

You can also use full Git URLs:
- **HTTPS**:  
    ```bash
    phpkg add https://github.com/owner/repo.git
    ```
- **SSH**:
    ```bash
    phpkg add git@github.com:owner/repo.git
    ```

Replace `owner` and `repo` with the real deal—e.g., `php-repos/observer`.

### Use an Alias

Set a shortcut with [Alias Command](https://phpkg.com/documentations/alias-command) first:
```bash
phpkg alias observer https://github.com/php-repos/observer.git
phpkg add observer
```

### Pick a Version

By default, `phpkg` grabs the latest release:
```bash
phpkg add php-repos/observer
# or
phpkg add https://github.com/php-repos/observer.git
```

- Want a specific tag? Pass the exact version number (complete version required):  
    ```bash
    phpkg add php-repos/observer v1.2.3
    # or with --version flag
    phpkg add php-repos/observer --version=v1.2.3
    ```
- Need the latest commit? Use development version:  
    ```bash
    phpkg add php-repos/observer --version=development
    ```
    This locks to the latest commit hash at the time of adding. Useful when no releases exist or you need the bleeding edge.

### GitHub Token Note

Busy project or private repo? `phpkg` needs a GitHub token to avoid rate limits or access locked code. Set `GITHUB_TOKEN` env var or use [Credential Command](https://phpkg.com/documentations/credential-command):

```bash
phpkg credential github.com <your-token>
```

---

### What Happens?

- **Package Location**: Lands in `Packages/owner/repo` (or your custom `packages-directory`).  
- **Config Update**: Adds to `phpkg.config.json`:  
    ```json
    {
        "packages": {
            "https://github.com/php-repos/observer.git": "v1.2.3"
        }
    }
    ```
- **Lock File**: Tracks metadata in `phpkg.config-lock.json`:  
    ```json
    {
        "https://github.com/php-repos/observer.git": {
            "version": "v1.2.3",
            "hash": "abc123...",
            "checksum": "def456...",
            "owner": "php-repos",
            "repo": "observer"
        }
    }
    ```
    The lock file includes version, commit hash, content checksum, owner, and repo information.
- **Next**: Run `phpkg build` to autoload its functions and classes.

---

## Examples

Add the `observer` package using simplified format:
```bash
phpkg add php-repos/observer
# or just
phpkg add observer
```

- Installs to `Packages/php-repos/observer`.  
- Updates configs with the latest release. If no releases exist, you'll need to use `--version=development` explicitly.

You can also use full URLs:
```bash
phpkg add https://github.com/php-repos/observer.git
```

Try a Composer package too:

```bash
phpkg add symfony/thanks
# or
phpkg add https://github.com/symfony/thanks.git
```

`phpkg` handles any Git repo—Composer or not.

---

## Tips

- **Rate Limits**: Lots of packages or releases? Add a token to keep it smooth.  
- **Versions**: Check repo tags online—`phpkg` picks what's there.  
- **Next Steps**: See [Build Command](https://phpkg.com/documentations/build-command) to use your new package.

---

## Related Commands

- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after adding packages
- **[Install Command](https://phpkg.com/documentations/install-command)** - Install packages from config file
- **[Update Command](https://phpkg.com/documentations/update-command)** - Update packages to new versions
- **[Remove Command](https://phpkg.com/documentations/remove-command)** - Remove packages from your project
- **[Alias Command](https://phpkg.com/documentations/alias-command)** - Create shortcuts for package URLs
- **[Credential Command](https://phpkg.com/documentations/credential-command)** - Manage Git credentials for private repos

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command
