# Remove Command

## Drop Packages with Ease

Need to ditch a package from your `phpkg` project? The `remove` command makes it simple to strip out any added package—whether by URL or alias—cleaning up your `packages-directory`, `phpkg.config.json`, and `phpkg.config-lock.json` in one go.

- **Why Use It?**: Keep your project lean and free of unused dependencies.
- **How It Works**: Targets the package and wipes its traces from your setup.

---

## Usage

Pass the package’s Git URL or an alias to `phpkg remove`:

### By URL
- **HTTPS**:
  ```bash
  phpkg remove https://github.com/owner/repo.git
  ```
- **SSH**:  
    ```bash
    phpkg remove git@github.com:owner/repo.git
    ```

### By Alias

Set an alias first with [Alias Command](https://phpkg.com/documentations/alias-command), then remove it:

```bash
phpkg alias tr https://github.com/php-repos/observer.git
phpkg remove tr
```

- **What Happens**: Deletes the package from your `packages-directory` (e.g., `Packages/`), removes it from `phpkg.config.json`’s `"packages"`, and clears its metadata from `phpkg.config-lock.json`.  
- _Tip_: Not sure of the URL? Check `"packages"` in `phpkg.config.json`.

---

## Examples

Say you added `observer` from `php-repos/observer`. To remove it:

### Using Simplified Format

```bash
phpkg remove php-repos/observer
# or just
phpkg remove observer
```

### Using Full URL

```bash
phpkg remove https://github.com/php-repos/observer.git
```

### Using an Alias

```bash
phpkg alias observer https://github.com/php-repos/observer.git
phpkg remove observer
```

- Result: `Packages/php-repos/observer/` is gone, and your config files are updated.

---

## Troubleshooting

### Error: `❌ The given identifier is invalid.`

**Cause**: Package identifier format is incorrect or package not found.

**Solutions**:
- Use the exact identifier from `phpkg.config.json`
- Try simplified format: `php-repos/observer` or just `observer`
- Use full URL if package was added with full URL
- Check `phpkg.config.json` for exact package identifier

**Example**:
```bash
# Check what's in config
cat phpkg.config.json

# Use exact identifier from config
phpkg remove https://github.com/php-repos/observer.git
```

### Error: `🔍 Package not found in your project.`

**Cause**: Package is not listed in `phpkg.config.json`.

**Solutions**:
- Check `phpkg.config.json` to see installed packages
- Verify package name/URL is correct
- Package might have been removed already
- Check if you're using the right identifier (alias vs URL)

**Example**:
```bash
# List packages in config
cat phpkg.config.json | grep packages

# Use correct identifier
phpkg remove package-name
```

### Package removed but files still exist

**Cause**: Manual deletion or files weren't removed properly.

**Solutions**:
- Manually delete package directory: `rm -rf Packages/owner/repo`
- Run `phpkg build` to refresh project
- Check if package is a dependency of another package

**Example**:
```bash
# Manual cleanup
rm -rf Packages/php-repos/observer
phpkg build  # Refresh project
```

### Error removing package with dependencies

**Cause**: Other packages might depend on this package.

**Solutions**:
- Check if other packages depend on it
- Remove dependent packages first
- Use `--force` flag if available (check command help)
- Review dependency tree in `phpkg.config-lock.json`

**Example**:
```bash
# Check dependencies
cat phpkg.config-lock.json

# Remove dependent packages first, then this one
```

### Config file not updated after removal

**Cause**: Write permissions issue or config file locked.

**Solutions**:
- Check file permissions: `ls -l phpkg.config.json`
- Ensure you have write access
- Verify config file is valid JSON
- Try running command again

**Example**:
```bash
# Check permissions
ls -l phpkg.config.json

# Fix permissions if needed
chmod 644 phpkg.config.json
phpkg remove package
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Verify Removal**: Peek at `Packages/` or `phpkg.config.json`—the package should be history.  
- **Next Step**: Run `phpkg build` to refresh your project without the removed package.  
- **Learn More**: See [Add Command](https://phpkg.com/documentations/add-command) for adding packages or [Alias Command](https://phpkg.com/documentations/alias-command) for shortcuts.

---

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages to your project
- **[Update Command](https://phpkg.com/documentations/update-command)** - Update packages to new versions
- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after removing packages
- **[Alias Command](https://phpkg.com/documentations/alias-command)** - Create shortcuts for package URLs
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
