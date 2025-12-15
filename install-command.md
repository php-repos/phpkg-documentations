# Install Command

## Sync Your Packages Anywhere

Once you've added packages to your project using `phpkg add`, the `install` command helps you set up the same packages elsewhere—like a teammate's machine or a server. It reads your `phpkg.config.json`, fetches the listed packages from Git, and installs them into your `packages-directory`. No need to clone repositories by hand!

- **Perfect For**: Replicating your setup across different machines.
- **How It Works**: Uses the `"packages"` section of your config to download the right versions.

---

## Usage

From your project's root directory, run:

```bash
phpkg install
```

- **What It Does**: Installs every package listed in `phpkg.config.json`'s `"packages"` section.  
- Where They Go: Places them in the directory set by `"packages-directory"` (defaults to `Packages/`).  
- No Directory?: Creates it automatically if it doesn't exist.

**Tip: Run `phpkg add` first to define your packages—`install` needs that list to work.**

---

## Why Use It?

- **Consistency**: Guarantees the same package versions everywhere.  
- **Efficiency**: One command beats manually fetching each package.  
- **Automation**: Streamlines setup for CI/CD or new developers.

After running, check your `packages-directory`—all your packages will be there, ready for the next step (like `phpkg build`).

## Examples

Imagine your `phpkg.config.json` looks like this:

```json
{
    "packages-directory": "vendor",
    "packages": {
        "https://github.com/php-repos/observer.git": "v1.0.0",
        "https://github.com/php-repos/datatype.git": "v2.5.0"
    }
}
```

Run `phpkg install`, and your `vendor/` directory will include:
- `php-repos/observer/` at version `v1.0.0`  
- `php-repos/datatype/` at version `v2.5.0`

**Next Step: Use `phpkg build` to autoload these packages into your project.**

---

## Troubleshooting

### Error: `📄 Could not read the project config.`

**Cause**: Missing or invalid `phpkg.config.json`.

**Solutions**:
- Run `phpkg init` to create config file
- Check if you're in project root directory
- Verify `phpkg.config.json` exists and is valid JSON

**Example**:
```bash
# Initialize if missing
phpkg init

# Then install
phpkg install
```

### Error: `📦 Could not read current dependencies for the project.`

**Cause**: Lock file missing or packages not properly configured.

**Solutions**:
- Run `phpkg add` for each package first
- Check `phpkg.config-lock.json` exists
- Verify packages are listed in `phpkg.config.json`
- Re-add packages if needed

**Example**:
```bash
# If packages are missing, add them
phpkg add php-repos/observer
phpkg install
```

### Packages not installing

**Cause**: Network issues, authentication, or invalid package URLs.

**Solutions**:
- Check internet connection
- Verify package URLs in `phpkg.config.json` are correct
- Add GitHub token for private repos: `phpkg credential github.com <token>`
- Use verbose mode: `phpkg -vv install`

**Example**:
```bash
phpkg -vv install  # See detailed error messages
```

### Some packages install, others fail

**Cause**: Individual package issues (network, auth, or invalid URL).

**Solutions**:
- Check which packages failed in verbose output
- Verify failed package URLs are correct
- Check if packages are private (need credentials)
- Try installing failed packages individually: `phpkg add package`

**Example**:
```bash
# Install all
phpkg install

# If one fails, try individually
phpkg add failed-package-url
```

### Version mismatch errors

**Cause**: Lock file specifies versions that don't exist.

**Solutions**:
- Update packages: `phpkg update package`
- Check if versions exist in repositories
- Use `--force` if available
- Regenerate lock file by removing and re-adding packages

**Example**:
```bash
# Update to fix version issues
phpkg update package-name
phpkg install
```

### Dependency resolution issues

**Cause**: Lock file (`phpkg.config-lock.json`) contains outdated or corrupted dependency information.

**Solutions**:
- Remove the lock file: `rm phpkg.config-lock.json`
- Run install again: `phpkg install`
- The lock file will be regenerated with correct dependency information
- If issues persist, also check `phpkg.config.json` for invalid package entries

**Example**:
```bash
# Remove corrupted lock file
rm phpkg.config-lock.json

# Reinstall (regenerates lock file)
phpkg install

# Verify it worked
ls phpkg.config-lock.json
```

### Permission errors

**Cause**: Cannot write to `packages-directory`.

**Solutions**:
- Check write permissions: `ls -ld Packages/`
- Fix permissions: `chmod 755 Packages/`
- Check if directory exists or can be created
- Verify disk space available

**Example**:
```bash
# Check permissions
ls -ld Packages/

# Fix if needed
chmod 755 Packages/
phpkg install
```

### Rate limit errors

**Cause**: GitHub API rate limits exceeded.

**Solutions**:
- Add GitHub token: `phpkg credential github.com <token>`
- Set environment variable: `export GITHUB_TOKEN=your_token`
- Wait for rate limit to reset
- Install packages in batches

**Example**:
```bash
phpkg credential github.com ghp_your_token_here
phpkg install
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Version Control**: Commit `phpkg.config.json` to Git to keep installs consistent across machines.  
- **Private Repos**: For GitHub tokens, set the `GITHUB_TOKEN` environment variable.  
- **Troubleshooting**: If a package doesn't install, verify it's listed in `phpkg.config.json`.

---

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages to your project
- **[Update Command](https://phpkg.com/documentations/update-command)** - Update packages to new versions
- **[Remove Command](https://phpkg.com/documentations/remove-command)** - Remove packages from your project
- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after installing packages
- **[Init Command](https://phpkg.com/documentations/init-command)** - Initialize a new phpkg project
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
