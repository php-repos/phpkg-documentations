# Alias Command

## Simplify Package Names

Tired of typing out long Git URLs for every `phpkg` command? The `alias` command lets you swap them for short, memorable names. Use aliases anywhere a package URL is needed—`add`, `remove`, `update`—and keep your workflow smooth.

---

## Usage

Set an alias with a name and its package URL:

```bash
phpkg alias <alias> <package-url>
```

### Example

```bash
phpkg alias datatype https://github.com/php-repos/datatype.git
```

Now use it like this:

```bash
phpkg add datatype
phpkg remove datatype
phpkg update datatype
```

- **Multiple Aliases**: Same package, different names? Go for it:
    ```bash
    phpkg alias observer https://github.com/php-repos/observer.git
    phpkg alias event-driven https://github.com/php-repos/observer.git
    phpkg alias ob https://github.com/php-repos/observer.git
    ```
- **Aliases are project-specific, stored in `phpkg.config.json`—unique per project.**

### Check Your Aliases

To see what aliases are set, check `phpkg.config.json` under the "aliases" section—aliases map to URLs there.

---

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages using aliases
- **[Remove Command](https://phpkg.com/documentations/remove-command)** - Remove packages using aliases
- **[Update Command](https://phpkg.com/documentations/update-command)** - Update packages using aliases
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Customization](https://phpkg.com/documentations/customization)** - Configure your phpkg project
