# Getting Started with phpkg

## Welcome to phpkg
phpkg is a lightweight PHP package manager that simplifies your workflow. Forget Composer’s complexity—`phpkg` autoloads namespaced functions and classes from Git repositories directly, with no central registry or bloated `vendor/` dirs. Whether you’re building apps or running scripts, `phpkg` empowers both object-oriented and functional programming, getting you coding faster.

- **Why phpkg?** No setup overload, instant Git integration, and the freedom to write lean functions without class wrappers.
- **Quick Start**: Try this now:
  ```bash
  bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"
  phpkg run https://github.com/php-repos/chuck-norris
  ```

See a Chuck Norris joke in your terminal—no config needed.

---

## Requirements

To use `phpkg`, ensure you have:
- PHP >= 8.1: With `php-mbstring` (for string handling), `php-zip` (for unpacking archives) and `php-curl` (for Git downloads).
- Git: To clone repositories directly.
- unzip: To extract package files.

*Works on Unix/Linux/macOS and Windows. Windows users need PHP 8.5 or later (PHP 8.5 is fully tested; later versions may need additional testing).*

## Installation

### Unix/Linux/macOS

Install `phpkg` with one command:

```shell
bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"
```

This downloads and sets up `phpkg` in your home directory. Open a new terminal to use it (path updated).

### Windows

Run this command in PowerShell to install `phpkg`:

```powershell
powershell -ExecutionPolicy Bypass -Command "Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.ps1' -OutFile install.ps1 -UseBasicParsing; powershell -ExecutionPolicy Bypass -File install.ps1"
```

This downloads and sets up `phpkg` in your home directory. Open a new terminal to use it (path updated).

---

## Usage

`phpkg` excels at managing packages and running standalone scripts. Here’s how to get started.

Set Up Your Project

1. **Initialize**: Create a new project:
    ```shell
    mkdir my-app && cd my-app
    phpkg init
    ```
    - Adds `Packages/` for dependencies, `phpkg.config.json` for settings, and `phpkg.config-lock.json` for metadata.

2. **Configure**: Map your namespaces in `phpkg.config.json`:
    ```json
   {
      "map": {"App": "src", "Tests": "tests"},
      "entry-points": ["public/index.php"],
      "packages": []
   }
   ```
    - `App\` → `src/`, `Tests\` → `tests/`.

3. **Add a Package**: Install from GitHub:
    ```shell
    phpkg add php-repos/observer
    ```
    - Clones `observer` to `Packages/`, updates configs with version and hash.
    - You can use simplified formats: `owner/repo` for GitHub packages (e.g., `php-repos/observer`) or just `repo` for php-repos packages (e.g., `observer`).
    - Full Git URLs also work: `https://github.com/php-repos/observer.git` or `git@github.com:php-repos/observer.git`.

    _No central repo—just Git URLs. Works with GitHub now, GitLab and others soon._

4. **Build**: Build your project:
    ```shell
    phpkg build
    ```
   - Creates `build/` directory with production-ready files, autoloads dependencies into entry points (e.g., `public/index.php`).

   _Watch changes live with `phpkg watch` to automatically rebuild on file changes._

**Add GitHub Token (Optional)**
For private repos, or when you have many dependencies, add a GitHub token:

```shell
phpkg credential github.com <your-token>
```

- Generate at [GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- Skip if `GITHUB_TOKEN` env var is set.

**Run Standalone Packages**
Execute scripts directly:

```shell
phpkg run php-repos/weather
```

- Outputs weather forecast in your terminal—no setup.
- You can use simplified formats: `owner/repo` for GitHub packages or just `repo` for php-repos packages.

---

## Example: Build a Simple App

1. **Init**: `phpkg init`
2. **Add Code**:
    ```php
    // src/Hello.php
    namespace App;
    function greet($name) { return "Hello, $name!"; }
    ```
   ```php
    // public/index.php
    require 'build/phpkg.imports.php';
    echo \App\greet('World');
    ```
3. **Build**: `phpkg build`
4. **Run**:
    ```shell
    cd build
    php public/index.php
    ```
   _Output: “Hello, World!”_

_`phpkg` autoloads namespaced functions like `App\greet`—no classes needed for simple tasks._

---

## Why phpkg?

- **Function-First Autoloading**: `phpkg` autoloads namespaced functions—not just classes—letting you write simple, reusable functions instead of wrapping everything in objects. Unlike Composer’s class-only PSR-4, this unlocks functional programming in PHP, making your code cleaner and more expressive.
- **Speed**: Installs in seconds, builds without bloat—no heavy `vendor/` dirs or lock files slowing you down.
- **Freedom**: Use any Git repo directly—no central registry or middleman locking you in.
- **Simplicity**: Minimal setup, maximum control—focus on coding, not configuring.

---

## Common Workflows

### Starting a New Project

```bash
# 1. Initialize
phpkg init

# 2. Add dependencies
phpkg add php-repos/observer
phpkg add owner/package-name

# 3. Build
phpkg build

# 4. Develop (with auto-rebuild)
phpkg watch
```

### Running Standalone Tools

```bash
# Run a CLI tool
phpkg run php-repos/weather

# Serve a web app
phpkg serve php-repos/daily-routine
```

### Updating Dependencies

```bash
# Update to latest
phpkg update php-repos/observer

# Update to specific version
phpkg update php-repos/observer v2.0.0
# or
phpkg update php-repos/observer --version=v2.0.0

# Update all (install after changes)
phpkg install
```

---

## Key Concepts

### Simplified Package Formats

phpkg supports simplified package identifiers:

- **GitHub packages**: `owner/repo` (e.g., `php-repos/observer`)
- **php-repos packages**: Just `repo` (e.g., `observer`)
- **Full URLs**: `https://github.com/owner/repo.git` or `git@github.com:owner/repo.git`

### Function-First Autoloading

Unlike Composer, phpkg autoloads **both** classes and functions:

```php
namespace App\Utils;

// This function is autoloaded!
function format($text) {
    return strtoupper($text);
}

// So is this class
class Formatter {
    // ...
}
```

### Build System

- **Build**: `phpkg build` → `build/` directory
- **Auto-rebuild**: `phpkg watch` monitors changes and rebuilds automatically

For deeper understanding, see [Concepts](https://phpkg.com/documentations/concepts).

---

## Related Documentation

- **[Installation](https://phpkg.com/documentations/installation)** - Install phpkg on your system
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Init Command](https://phpkg.com/documentations/init-command)** - Initialize a new phpkg project
- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages to your project
- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
