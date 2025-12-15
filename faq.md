# Frequently Asked Questions (FAQ)

Common questions about phpkg.

---

## General Questions

### What is phpkg?

phpkg is a lightweight PHP package manager that:
- Manages dependencies directly from Git repositories
- Autoloads namespaced functions (not just classes)
- Provides a build system for PHP projects
- Allows running packages standalone without installation

### How is phpkg different from Composer?

| Feature | phpkg | Composer |
|---------|-------|----------|
| Function autoloading | ✅ Yes | ❌ No |
| Central registry | ❌ No | ✅ Packagist |
| Git-based | ✅ Direct | ⚠️ Via registry |
| Build system | ✅ Built-in | ❌ External |
| Standalone execution | ✅ Yes | ❌ No |

### Do I need to uninstall Composer to use phpkg?

No! phpkg and Composer can coexist. They use different config files and don't interfere with each other.

### Can I use phpkg with existing Composer projects?

Yes! Use `phpkg migrate` to convert `composer.json` to `phpkg.config.json`. You can also use both side-by-side.

---

## Installation

### What are the system requirements?

- **PHP**: >= 8.1 (8.5+ for Windows)
- **Extensions**: `php-mbstring`, `php-zip`, `php-curl`
- **Git**: For cloning repositories
- **unzip**: For extracting archives

### Does phpkg work on Windows?

Yes! Windows is supported with PHP 8.5 or later. PHP 8.5 is fully tested; later versions may need additional testing.

Use `install.ps1` instead of `install.sh` on Windows.

### Why do I need to restart my terminal after installation?

The installation script adds phpkg to your PATH, which requires a new shell session to take effect. Alternatively, run `source ~/.bashrc` (or `~/.zshrc`).

### Can I install phpkg globally?

Yes! phpkg installs to `~/.phpkg` (Unix) or `%USERPROFILE%\.phpkg` (Windows), making it available system-wide.

---

## Package Management

### How do I add a package?

```bash
# Simplified format (recommended)
phpkg add php-repos/observer
phpkg add owner/repo

# Full URL
phpkg add https://github.com/owner/repo.git
```

### What's the difference between simplified formats?

- `owner/repo` → Assumes GitHub (e.g., `php-repos/observer`)
- `repo` → Assumes php-repos organization (e.g., `observer` → `php-repos/observer`)

### Can I use private repositories?

Yes! Add a GitHub token:
```bash
phpkg credential github.com <your-token>
```

Or set `GITHUB_TOKEN` environment variable.

### How do I specify a version?

```bash
# Latest version (default)
phpkg add package

# Specific version (complete version number required)
phpkg add package v1.2.3
# or
phpkg add package --version=v1.2.3

# Development version
phpkg add package --version=development
```

### What if a package has no releases?

Use the development version:
```bash
phpkg add package --version=development
```

This locks to the latest commit hash at the time of adding. The commit hash is stored in your `phpkg.config-lock.json`, so it's pinned to that specific commit until you update it.

### Can I use packages from GitLab or Bitbucket?

Currently, GitHub is fully supported. GitLab and other Git hosts are planned.

### How do I remove a package?

```bash
phpkg remove package
# or
phpkg remove https://github.com/owner/repo.git
```

### How do I update a package?

```bash
# Update to latest
phpkg update package

# Update to specific version
phpkg update package --version=v2.0.0
```

### What's the difference between `add` and `install`?

- **`add`**: Adds a package to your config and installs it
- **`install`**: Installs packages already listed in `phpkg.config.json`

Use `install` when:
- Cloning a project that already has `phpkg.config.json`
- After manually editing the config file
- In CI/CD pipelines

---

## Build System

### What does `phpkg build` do?

1. Reads `phpkg.config.json`
2. Copies source files to `build/` directory
3. Copies installed packages
4. Generates `phpkg.imports.php` with autoloading
5. Injects autoloading into entry points

### Do I need to rebuild after every change?

Yes, unless you use `phpkg watch` which auto-rebuilds on file changes.

### Why do I need to rebuild?

phpkg generates autoload files and injects them into entry points. Without rebuilding, new code won't be autoloaded.

### Can I customize the build output?

Yes! Configure in `phpkg.config.json`:
- `packages-directory`: Where packages are stored
- `excludes`: Files/directories to exclude
- `import-file`: Name of autoload file

---

## Autoloading

### How does function autoloading work?

phpkg scans your code, finds namespaced functions and constants, and adds `require_once` statements directly in the files where they are used. For classes, it generates an autoload file (`phpkg.imports.php`) that is included in entry points.

```php
// src/Utils.php
namespace App\Utils;

function format($text) {
    return strtoupper($text);
}

// Usage (after build)
\App\Utils\format("hello");  // Works!
```

### Do I need to require files manually?

No! After building, just use your entry points. phpkg injects this automatically.

### Can I use both classes and functions?

Yes! phpkg autoloads both:

```php
namespace App;

// Function
function greet($name) { return "Hello, $name!"; }

// Class
class User {
    // ...
}
```

### How do namespace mappings work?

```json
{
  "map": {
    "App": "src"
  }
}
```

This means `App\` namespace maps to `src/` directory:
- `App\User` → `src/User.php`
- `App\Utils\format` → `src/Utils/format.php` (function)

---

## Standalone Execution

### What's the difference between `run` and `serve`?

- **`run`**: Executes package as CLI tool (terminal output)
- **`serve`**: Runs package as web app (HTTP server)

### Do I need to install packages to run them?

No! `phpkg run` and `phpkg serve` download and execute packages without adding them to your project.

### Can I pass arguments to `phpkg run`?

Yes! Arguments after the entry point are passed to the script:
```bash
phpkg run package entry.php arg1 arg2
```

### How do I stop `phpkg serve`?

Press `Ctrl+C`. On Unix systems, phpkg handles signals gracefully.

---

## Configuration

### What's the difference between `phpkg.config.json` and `phpkg.config-lock.json`?

- **`phpkg.config.json`**: Your configuration (version control this)
- **`phpkg.config-lock.json`**: Locked versions and metadata (version control this)

The lock file ensures everyone gets the same package versions.

### Should I commit the lock file?

Yes! Commit both `phpkg.config.json` and `phpkg.config-lock.json` to ensure consistent builds across environments.

### Can I edit config files manually?

Yes, but be careful with JSON syntax. After editing, run `phpkg build` or `phpkg install` to apply changes.

### What are aliases for?

Aliases create shortcuts for long package URLs:

```bash
phpkg alias observer https://github.com/php-repos/observer.git
phpkg add observer  # Instead of full URL
```

---

## Troubleshooting

### Package not found?

1. Check the format: `owner/repo` or full URL
2. Verify repository exists on GitHub
3. Check if it's a private repo (needs token)

### Build fails?

1. Check `phpkg.config.json` syntax
2. Verify entry points exist
3. Run `phpkg -vv build` for verbose output
4. Check namespace mappings match your code

### Autoloading not working?

1. Ensure you've run `phpkg build`
2. Check entry point includes `phpkg.imports.php`
3. Verify namespace mappings in config
4. Check file structure matches namespace

### Rate limit errors?

Add a GitHub token:
```bash
phpkg credential github.com <token>
```

### Still having issues?

See the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting) for detailed solutions.

---

## Best Practices

### Should I use simplified formats or full URLs?

**Simplified formats** (`owner/repo`) are recommended:
- Shorter and cleaner
- Easier to read
- Less error-prone

Use **full URLs** when:
- Using non-GitHub repositories
- Need SSH instead of HTTPS
- Working with specific branches

### When should I use aliases?

Use aliases for:
- Frequently used packages
- Long package URLs
- Team consistency

### How do I optimize my build?

Use the `excludes` configuration in `phpkg.config.json` to exclude unnecessary files:

```json
{
  "excludes": [
    "node_modules",
    "docs"
  ]
}
```

This reduces build size and improves performance.

### How do I manage versions?

- Use semantic versioning in packages
- Pin versions for stable releases: `phpkg add package v1.2.3` (complete version number required, can omit `--version` flag)
- Use latest release by omitting version, or use `--version=development` for latest commit
- Commit lock file for consistency

---

## Advanced Topics

### Can I use phpkg in CI/CD?

Yes! Example GitHub Actions:

```yaml
- name: Install phpkg
  run: bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"

- name: Install dependencies
  run: phpkg install

- name: Build
  run: phpkg build
```

### How do I handle monorepos?

phpkg works with monorepos. Each package can have its own `phpkg.config.json`. Use relative paths or Git URLs to reference sibling packages.

### Can I create my own packages?

Yes! Create a repository with:
1. `phpkg.config.json` (optional, for package config)
2. Your PHP code with namespaces
3. Git tags for versions

Then others can use it:
```bash
phpkg add your-username/your-package
```

### How do I publish a package?

1. Push code to GitHub
2. Create releases/tags for versions
3. Share the repository URL
4. Others can use: `phpkg add owner/repo`

No registration or approval needed!

---

## Performance

### How can I speed up builds?

1. Add large directories to `excludes`
2. Reduce package count
3. Use `phpkg watch` instead of manual rebuilds
4. Exclude unnecessary files in config

---

## Migration

### Can I migrate from Composer?

Yes! Use `phpkg migrate` to convert `composer.json` to `phpkg.config.json`.

Note: Function autoloading won't work for Composer packages that don't use phpkg.

### Can I use both Composer and phpkg?

Yes! They can coexist. Use Composer for packages that need it, phpkg for others.

---

## Still Have Questions?

- Check the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting)
- Review [Concepts](https://phpkg.com/documentations/concepts) for deeper understanding
- See [Best Practices](https://phpkg.com/documentations/best-practices) for recommendations
- Review command-specific documentation
