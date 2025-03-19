## Remove Command

### Drop Packages with Ease

Need to ditch a package from your `phpkg` project? The `remove` command makes it simple to strip out any added package—whether by URL or alias—cleaning up your `packages-directory`, `phpkg.config.json`, and `phpkg.config-lock.json` in one go.

- **Why Use It?**: Keep your project lean and free of unused dependencies.
- **How It Works**: Targets the package and wipes its traces from your setup.

---

### Usage

Pass the package’s Git URL or an alias to `phpkg remove`:

#### By URL
- **HTTPS**:
  ```bash
  phpkg remove https://github.com/owner/repo.git
  ```
- **SSH**:  
    ```bash
    phpkg remove git@github.com:owner/repo.git
    ```

#### By Alias

Set an alias first with [Alias Command](https://phpkg.com/documentations/alias-command), then remove it:

```bash
phpkg alias tr https://github.com/php-repos/test-runner.git
phpkg remove tr
```

- **What Happens**: Deletes the package from your `packages-directory` (e.g., `Packages/`), removes it from `phpkg.config.json`’s `"packages"`, and clears its metadata from `phpkg.config-lock.json`.  
- _Tip_: Not sure of the URL? Check `"packages"` in `phpkg.config.json`.

---

#### Example

Say you added `test-runner` from `php-repos/test-runner`. To remove it:

##### Using the URL

```bash
phpkg remove https://github.com/php-repos/test-runner.git
```

##### Using an Alias

```bash
phpkg alias test-runner https://github.com/php-repos/test-runner.git
phpkg remove test-runner
```

- Result: `Packages/php-repos/test-runner/` is gone, and your config files are updated.

---

### Tips

- **Verify Removal**: Peek at `Packages/` or `phpkg.config.json`—the package should be history.  
- **Next Step**: Run `phpkg build` to refresh your project without the removed package.  
- **Learn More**: See [Add Command](https://phpkg.com/documentations/add-command) for adding packages or [Alias Command](https://phpkg.com/documentations/alias-command) for shortcuts.
