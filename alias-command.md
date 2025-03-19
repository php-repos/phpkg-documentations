## Alias Command

### Simplify Package Names

Tired of typing out long Git URLs for every `phpkg` command? The `alias` command lets you swap them for short, memorable names. Use aliases anywhere a package URL is needed—`add`, `remove`, `update`—and keep your workflow smooth.

---

### Usage

Set an alias with a name and its package URL:

```bash
phpkg alias <alias> <package-url>
```

#### Example:

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
    phpkg alias test-runner https://github.com/php-repos/test-runner.git
    phpkg alias tests https://github.com/php-repos/test-runner.git
    phpkg alias tr https://github.com/php-repos/test-runner.git
    ```
- **Aliases are project-specific, stored in `phpkg.config.json`—unique per project.**

#### Check Your Aliases

See what’s set:

```bash
phpkg alias list  # Coming soon—check your config for now
```

Or peek at `phpkg.config.json` under "aliases"—aliases map to URLs there.
Ready to add a package? See [Add Command](https://phpkg.com/documentations/add-command).
