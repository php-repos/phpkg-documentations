## Update Command

### Keep Your Packages Fresh

Packages evolve—new versions bring fixes, features, or performance boosts. The `phpkg update` command lets you effortlessly upgrade a package in your project to the latest version or a specific tag, ensuring you’re always running the best fit for your needs.

- **Why Use It?**: Stay current without the grunt work.
- **How It Works**: Syncs your `packages-directory` and config files with the desired version.

---

### Usage

Pass the package’s Git URL or an alias to `phpkg update`:

#### By URL

- **Latest Version**:
  ```bash
  phpkg update https://github.com/owner/repo.git
  ```
- **Specific Version**:  
    ```bash
    phpkg update https://github.com/owner/repo.git --version=v1.2.3
    ```

#### By Alias

Set an alias with [Alias Command](https://phpkg.com/documentations/alias-command), then update:  

```bash
phpkg alias my-package https://github.com/owner/repo.git
phpkg update my-package  # Latest
phpkg update my-package --version=v1.2.3  # Specific
```

- **What Happens**: Updates the package in your `packages-directory` (e.g., `Packages/`), refreshes `phpkg.config.json`’s `"packages"`, and syncs `phpkg.config-lock.json`.

---

### Example

Say you’ve got `test-runner` from `php-repos/test-runner` in your project:

#### Update to Latest

```bash
phpkg update https://github.com/php-repos/test-runner.git
```

- Pulls the newest release.

#### Update to a Version

```bash
phpkg update https://github.com/php-repos/test-runner.git --version=v1.0.1
```

- Locks to `v1.0.1`.

#### Using an Alias

```bash
phpkg alias test-runner https://github.com/php-repos/test-runner.git
phpkg update test-runner  # Latest
phpkg update test-runner --version=v1.0.1  # Specific
```

- Result: Your `Packages/php-repos/test-runner/` and config files reflect the updated version.

---

### Tips

- **Check Versions**: See available tags on the package’s Git repo.  
- **Rebuild**: Run `phpkg build` after updating to apply changes—see [Build Command](https://phpkg.com/documentations/build-command).  
- **Aliases**: Simplify with shortcuts—learn more at [Alias Command](https://phpkg.com/documentations/alias-command).  
- **Tokens**: Rate-limited? Add a GitHub token via [Credential Command](https://phpkg.com/documentations/credential-command).
