## Install Command

### Sync Your Packages Anywhere

Once you’ve added packages to your project using `phpkg add`, the `install` command helps you set up the same environment elsewhere—like a teammate’s machine or a production server. It reads your `phpkg.config.json`, fetches the listed packages from Git, and installs them into your `packages-directory`. No need to clone repositories by hand!

- **Perfect For**: Replicating your setup across environments.
- **How It Works**: Uses the `"packages"` section of your config to download the right versions.

---

### Usage

From your project’s root directory, run:

```bash
phpkg install
```

- **What It Does**: Installs every package listed in `phpkg.config.json`’s `"packages"` section.  
- Where They Go: Places them in the directory set by `"packages-directory"` (defaults to `Packages/`).  
- No Directory?: Creates it automatically if it doesn’t exist.

**Tip: Run `phpkg add` first to define your packages—`install` needs that list to work.**

---

### Why Use It?

- **Consistency**: Guarantees the same package versions everywhere.  
- **Efficiency**: One command beats manually fetching each package.  
- **Automation**: Streamlines setup for CI/CD or new developers.

After running, check your `packages-directory`—all your packages will be there, ready for the next step (like `phpkg build`).

### Example

Imagine your `phpkg.config.json` looks like this:

```json
{
    "packages-directory": "vendor",
    "packages": {
        "https://github.com/php-repos/test-runner.git": "v1.0.0",
        "https://github.com/php-repos/datatype.git": "v2.5.0"
    }
}
```

Run `phpkg install`, and your `vendor/` directory will include:
- `php-repos/test-runner/` at version `v1.0.0`  
- `php-repos/datatype/` at version `v2.5.0`

**Next Step: Use `phpkg build` to autoload these packages into your project.**

---

### Tips

- **Version Control**: Commit `phpkg.config.json` to Git to keep installs consistent across machines.  
- **Private Repos**: For GitHub tokens, set the `GITHUB_TOKEN` environment variable.  
- **Troubleshooting**: If a package doesn’t install, verify it’s listed in `phpkg.config.json`.

For more on managing packages, see the [Add Command documentation](https://phpkg.com/documentations/add-command).
