# Command Comparison Guide

When to use which phpkg command.

---

## Package Management Commands

### `add` vs `update` vs `remove` vs `install`

| Command | When to Use | What It Does |
|---------|-------------|--------------|
| **`add`** | Adding a new package | Adds package to config + installs it |
| **`update`** | Updating existing package | Updates package to new version |
| **`remove`** | Removing a package | Removes package from config + deletes files |
| **`install`** | Installing from config | Installs packages listed in config |

#### Decision Tree

```
Need to add a new package?
├─ Yes → phpkg add package
└─ No → Continue

Need to update existing package?
├─ Yes → phpkg update package
└─ No → Continue

Need to remove a package?
├─ Yes → phpkg remove package
└─ No → Continue

Have phpkg.config.json but packages not installed?
├─ Yes → phpkg install
└─ No → Done
```

#### Examples

**Adding a new package**:
```bash
phpkg add php-repos/observer
```

**Updating existing package**:
```bash
phpkg update php-repos/observer
```

**Removing a package**:
```bash
phpkg remove php-repos/observer
```

**Installing from config** (after cloning project):
```bash
git clone project
cd project
phpkg install  # Installs all packages from config
```

---

## Build Commands

### `build` vs `watch` vs `flush`

| Command | When to Use | What It Does |
|---------|-------------|--------------|
| **`build`** | Manual build needed | Builds project once |
| **`watch`** | During development | Auto-rebuilds on file changes |
| **`flush`** | Clean up builds | Removes build artifacts |

#### Decision Tree

```
During active development?
├─ Yes → phpkg watch (auto-rebuilds)
└─ No → Continue

Need one-time build?
├─ Yes → phpkg build
└─ No → Continue

Need to clean build artifacts?
├─ Yes → phpkg flush
└─ No → Done
```

#### Examples

**One-time build**:
```bash
phpkg build
```

**Auto-rebuild during development**:
```bash
phpkg watch                    # Watches and rebuilds automatically
```

**Clean up**:
```bash
phpkg flush                    # Removes build/ directory
```

---

## Standalone Execution Commands

### `run` vs `serve`

| Command | When to Use | What It Does |
|---------|-------------|--------------|
| **`run`** | CLI tools, scripts | Executes package as command-line tool |
| **`serve`** | Web apps, dashboards | Serves package as web application |

#### Decision Tree

```
What type of package?
├─ CLI tool / script → phpkg run package
└─ Web app / dashboard → phpkg serve package
```

#### Examples

**Running a CLI tool**:
```bash
phpkg run php-repos/weather
phpkg run phpstan/phpstan analyze ./src
```

**Serving a web app**:
```bash
phpkg serve php-repos/daily-routine
# Opens http://localhost:8000
```

---

## Project Setup Commands

### `init` vs `migrate`

| Command | When to Use | What It Does |
|---------|-------------|--------------|
| **`init`** | Starting new project | Creates phpkg.config.json from scratch |
| **`migrate`** | Converting from Composer | Converts composer.json to phpkg.config.json |

#### Decision Tree

```
Starting new project?
├─ Yes → phpkg init
└─ No → Continue

Converting from Composer?
├─ Yes → phpkg migrate
└─ No → Done
```

#### Examples

**New project**:
```bash
mkdir my-app
cd my-app
phpkg init
```

**Migrating from Composer**:
```bash
cd existing-composer-project
phpkg migrate  # Converts composer.json
```

---

## Utility Commands

### `version` vs `alias` vs `credential`

| Command | When to Use | What It Does |
|---------|-------------|--------------|
| **`version`** | Check installation | Displays phpkg version information |
| **`alias`** | Creating shortcuts | Creates alias for package URL |
| **`credential`** | Authentication | Stores Git credentials/tokens |

#### Decision Tree

```
Need to check version?
├─ Yes → phpkg version
└─ No → Continue

Need shortcut for package URL?
├─ Yes → phpkg alias name url
└─ No → Continue

Need to authenticate?
├─ Yes → phpkg credential github.com token
└─ No → Done
```

#### Examples

**Checking version**:
```bash
phpkg version
# Output: phpkg version 3.0.0
```

**Creating alias**:
```bash
phpkg alias observer https://github.com/php-repos/observer.git
phpkg add observer  # Use alias instead of URL
```

**Adding credentials**:
```bash
phpkg credential github.com <your-token>
```

---

## Common Workflows

### Starting a New Project

```bash
# 1. Initialize
phpkg init

# 2. Add dependencies
phpkg add package1
phpkg add package2

# 3. Build
phpkg build

# 4. Develop (with auto-rebuild)
phpkg watch
```

### Cloning an Existing Project

```bash
# 1. Clone
git clone project
cd project

# 2. Install dependencies
phpkg install

# 3. Build
phpkg build
```

### Updating Dependencies

```bash
# Update specific package
phpkg update package

# Or update all (after manual config edit)
phpkg install
```

### Running Standalone Tools

```bash
# CLI tool
phpkg run tool-package

# Web app
phpkg serve web-app-package
```

### Deployment Workflow

```bash
# 1. Install dependencies
phpkg install

# 2. Build project
phpkg build

# 3. Deploy build/ directory
```

---

## Command Combinations

### Active Development Workflow

```bash
phpkg watch  # In one terminal (auto-rebuilds)
# Edit code in another terminal
```

### Testing Updates

```bash
phpkg update package
phpkg build
# Run tests
```

### Clean Rebuild

```bash
phpkg flush
phpkg install
phpkg build
```

### Migrating and Building

```bash
phpkg migrate
phpkg install
phpkg build
```

---

## Quick Reference

| Need | Command |
|------|---------|
| Start new project | `phpkg init` |
| Add package | `phpkg add package` |
| Update package | `phpkg update package` |
| Remove package | `phpkg remove package` |
| Install from config | `phpkg install` |
| Build once | `phpkg build` |
| Auto-rebuild | `phpkg watch` |
| Clean builds | `phpkg flush` |
| Run CLI tool | `phpkg run package` |
| Serve web app | `phpkg serve package` |
| Check version | `phpkg version` |
| Create alias | `phpkg alias name url` |
| Add credentials | `phpkg credential host token` |
| Migrate from Composer | `phpkg migrate` |

---

## Decision Matrix

### When to Use Each Command

| Scenario | Command |
|----------|---------|
| First time setting up project | `init` |
| Adding new dependency | `add` |
| Updating existing dependency | `update` |
| Removing dependency | `remove` |
| Cloning project, need dependencies | `install` |
| Building project | `build` |
| Auto-rebuild during dev | `watch` |
| Cleaning build artifacts | `flush` |
| Running one-off CLI tool | `run` |
| Testing web app locally | `serve` |
| Checking phpkg version | `version` |
| Shortening long URLs | `alias` |
| Accessing private repos | `credential` |
| Converting Composer project | `migrate` |

---

## Tips

1. **Use `watch` during development** - Saves time
2. **Use `install` after cloning** - Gets all dependencies
3. **Use `build` before deploying** - Ensures all dependencies included
4. **Use `alias` for common packages** - Consistency
5. **Use `run`/`serve` for testing** - No installation needed

---

For detailed information on each command, see:
- [Add Command](https://phpkg.com/documentations/add-command)
- [Remove Command](https://phpkg.com/documentations/remove-command)
- [Update Command](https://phpkg.com/documentations/update-command)
- [Install Command](https://phpkg.com/documentations/install-command)
- [Init Command](https://phpkg.com/documentations/init-command)
- [Build Command](https://phpkg.com/documentations/build-command)
- [Watch Command](https://phpkg.com/documentations/watch-command)
- [Flush Command](https://phpkg.com/documentations/flush-command)
- [Run Command](https://phpkg.com/documentations/run-command)
- [Serve Command](https://phpkg.com/documentations/serve-command)
- [Version Command](https://phpkg.com/documentations/version-command)
- [Alias Command](https://phpkg.com/documentations/alias-command)
- [Credential Command](https://phpkg.com/documentations/credential-command)
- [Migrate Command](https://phpkg.com/documentations/migrate-command)

---

## Related Documentation

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
