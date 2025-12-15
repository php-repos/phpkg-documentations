# Init Command

## Kickstart Your phpkg Project

Ready to manage dependencies with `phpkg`? The `init` command sets up your project in seconds, creating the foundation for autoloading functions and classes from Git repos—no Composer clutter needed.

## Usage
Run this in your project's root directory:
```bash
phpkg init
```

- **What It Does**:
    - Creates `phpkg.config.json`: Configures your namespace mappings and settings.
    - Creates `phpkg.config-lock.json`: Tracks your added packages' versions and metadata.
    - Adds a `Packages/` directory: Stores source code for packages you install.

Want a custom packages directory? Use:

```shell
phpkg init --packages-directory=vendor
```

- Renames `Packages/` to `vendor/` (or any name you pick).

---

## Next Steps

After running `init`, tweak `phpkg.config.json` to map your code (e.g., `App` → `src/`). Example:

```json
{
    "map": {"App": "src"},
    "entry-points": ["public/index.php"],
    "packages": []
}
```

Then, add packages with `phpkg add` and build with `phpkg build`. See [Customization](https://phpkg.com/documentations/customization) for details.

## Examples

```bash
# 1. Initialize project
phpkg init

# 2. Configure namespaces (edit phpkg.config.json)
# 3. Add dependencies
phpkg add php-repos/observer

# 4. Build
phpkg build

# 5. Start developing
phpkg watch
```

## Tips

- **Custom packages directory**: Use `--packages-directory=vendor` to match Composer conventions
- **Entry points**: Set `entry-points` in config for web apps or CLI tools
- **Namespace mapping**: Map namespaces to match your directory structure
- **See also**: [Getting Started](https://phpkg.com/documentations/getting-started) for a complete walkthrough

---

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages after initializing
- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after setup
- **[Customization](https://phpkg.com/documentations/customization)** - Configure your phpkg project
- **[Migrate Command](https://phpkg.com/documentations/migrate-command)** - Migrate from Composer
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Complete walkthrough of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
