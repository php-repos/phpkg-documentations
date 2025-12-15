# Update Command

## Keep Your Packages Fresh

Packages evolve—new versions bring fixes, features, or performance boosts. The `phpkg update` command lets you effortlessly upgrade a package in your project to the latest version or a specific tag, ensuring you're always running the best fit for your needs.

- **Why Use It?**: Stay current without the grunt work.
- **How It Works**: Syncs your `packages-directory` and config files with the desired version.

---

## Usage

Pass the package identifier (simplified format or full Git URL) or an alias to `phpkg update`:

### Simplified Formats

For GitHub packages, you can use the `owner/repo` format:
```bash
phpkg update php-repos/observer
phpkg update owner/repo
```

For packages in the `php-repos` organization, you can use just the repo name:
```bash
phpkg update observer
phpkg update datatype
```

### Full Git URLs

- **Latest Version**:
  ```bash
  phpkg update https://github.com/owner/repo.git
  ```
- **Specific Version** (complete version number required):  
    ```bash
    phpkg update https://github.com/owner/repo.git v1.2.3
    # or with --version flag
    phpkg update https://github.com/owner/repo.git --version=v1.2.3
    ```

### By Alias

Set an alias with [Alias Command](https://phpkg.com/documentations/alias-command), then update:  

```bash
phpkg alias my-package https://github.com/owner/repo.git
phpkg update my-package  # Latest
phpkg update my-package --version=v1.2.3  # Specific
```

- **What Happens**: Updates the package in your `packages-directory` (e.g., `Packages/`), refreshes `phpkg.config.json`'s `"packages"`, and syncs `phpkg.config-lock.json`.

---

## Examples

Say you've got `observer` from `php-repos/observer` in your project:

### Update to Latest

Using simplified format:
```bash
phpkg update php-repos/observer
# or just
phpkg update observer
```

Using full URL:
```bash
phpkg update https://github.com/php-repos/observer.git
```

- Pulls the newest release.

### Update to a Version

```bash
phpkg update php-repos/observer v1.0.1
# or
phpkg update https://github.com/php-repos/observer.git v1.0.1
# or with --version flag
phpkg update php-repos/observer --version=v1.0.1
```

- Locks to `v1.0.1` (complete version number required).

### Using an Alias

```bash
phpkg alias observer https://github.com/php-repos/observer.git
phpkg update observer           # Latest
phpkg update observer v1.0.1    # Specific version (complete version required)
```

- Result: Your `Packages/php-repos/observer/` and config files reflect the updated version.

### Update to Development Version

If you're using a development version (latest commit), update it to get the newest commit hash:

```bash
phpkg update php-repos/observer --version=development
# or
phpkg update observer --version=development
```

- **What Happens**: Updates the package to the latest commit hash available at that moment and updates the commit hash in your `phpkg.config-lock.json`.
- **Note**: For development version, you must use the `--version=development` flag. For tagged versions, you can pass the version as a positional argument (e.g., `phpkg update package v1.2.3`).

---

## Troubleshooting

### Error: `🔍 Package not found in your project.`

**Cause**: Package is not currently installed in your project.

**Solutions**:
- Use `phpkg add` instead if package isn't installed: `phpkg add package`
- Check `phpkg.config.json` to see installed packages
- Verify package identifier is correct
- Package might have been removed

**Example**:
```bash
# Check installed packages
cat phpkg.config.json

# If not installed, add it first
phpkg add package
```

### Error: `❌ The given identifier is invalid.`

**Cause**: Package identifier format is incorrect.

**Solutions**:
- Use the exact identifier from `phpkg.config.json`
- Try simplified format: `php-repos/observer`
- Use full URL if that's how it was added
- Check for typos

**Example**:
```bash
# Check how package was added
cat phpkg.config.json

# Use matching format
phpkg update php-repos/observer
```

### Error: Version not found

**Cause**: Specified version doesn't exist in repository.

**Solutions**:
- Check available versions on GitHub releases page
- Use exact version number: `phpkg update package v1.2.3` (complete version required)
- Omit version to get latest: `phpkg update package`
- Verify version tag exists in repository

**Example**:
```bash
# Update to latest (no version specified)
phpkg update php-repos/observer

# Or use exact version
phpkg update php-repos/observer --version=v1.2.3
```

### Error: Rate limit exceeded

**Cause**: GitHub API rate limits.

**Solutions**:
- Add GitHub token: `phpkg credential github.com <token>`
- Set environment variable: `export GITHUB_TOKEN=your_token`
- Wait for rate limit to reset

**Example**:
```bash
phpkg credential github.com ghp_your_token_here
phpkg update package
```

### Update doesn't seem to work

**Cause**: Package updated but project not rebuilt.

**Solutions**:
- Run build after update: `phpkg build`
- Check `phpkg.config-lock.json` to verify version changed
- Clear builds and rebuild: `phpkg flush && phpkg build`

**Example**:
```bash
phpkg update package
phpkg build  # Required to apply changes
```

### Error: `📦 Could not get package and its dependencies.`

**Cause**: Network issue, authentication problem, or repository access issue.

**Solutions**:
- Check internet connection
- Verify repository is accessible
- Add credentials for private repos
- Use verbose mode: `phpkg -vv update package`

**Example**:
```bash
phpkg -vv update package  # See detailed error messages
```

### Version conflict with dependencies

**Cause**: Updated version conflicts with other packages.

**Solutions**:
- Check dependency requirements in `phpkg.config-lock.json`
- Update dependent packages first
- Use `--force` if available (check command help)
- Review compatibility requirements

**Example**:
```bash
# Check dependencies
cat phpkg.config-lock.json

# Update conflicting packages
phpkg update dependent-package
phpkg update package
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Check Versions**: See available tags on the package's Git repo.  
- **Rebuild**: Run `phpkg build` after updating to apply changes—see [Build Command](https://phpkg.com/documentations/build-command).  
- **Aliases**: Simplify with shortcuts—learn more at [Alias Command](https://phpkg.com/documentations/alias-command).  
- **Tokens**: Rate-limited? Add a GitHub token via [Credential Command](https://phpkg.com/documentations/credential-command).

---

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add new packages to your project
- **[Remove Command](https://phpkg.com/documentations/remove-command)** - Remove packages from your project
- **[Install Command](https://phpkg.com/documentations/install-command)** - Install packages from config file
- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after updating
- **[Alias Command](https://phpkg.com/documentations/alias-command)** - Create shortcuts for package URLs
- **[Credential Command](https://phpkg.com/documentations/credential-command)** - Manage Git credentials
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
