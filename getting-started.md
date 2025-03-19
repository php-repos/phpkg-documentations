## Getting Started with phpkg

### Welcome to phpkg
phpkg is a lightweight PHP package manager that simplifies your workflow. Forget Composer’s complexity—`phpkg` autoloads namespaced functions and classes from Git repositories directly, with no central registry or bloated `vendor/` dirs. Whether you’re building apps or running scripts, `phpkg` empowers both object-oriented and functional programming, getting you coding faster.

- **Why phpkg?** No setup overload, instant Git integration, and the freedom to write lean functions without class wrappers.
- **Quick Start**: Try this now:
  ```bash
  bash -c "$(curl -fsSL https://raw.github.com/php-repos/phpkg-installation/master/install.sh)"
  phpkg run https://github.com/php-repos/chuck-norris
  ```

See a Chuck Norris joke in your terminal—no config needed.

---

### Requirements

To use `phpkg`, ensure you have:
- PHP >= 8.1: With `php-mbstring` (for string handling), `php-zip` (for unpacking archives) and `php-curl` (for Git downloads).
- Git: To clone repositories directly.
- unzip: To extract package files.

Windows support coming soon—currently works on Unix/Linux/macOS.

### Installation

Install `phpkg` with one command:

```shell
bash -c "$(curl -fsSL https://raw.github.com/php-repos/phpkg-installation/master/install.sh)"
```

This downloads and sets up `phpkg` in your home directory. Open a new terminal to use it (path updated).

---

### Usage

`phpkg` excels at managing packages and running standalone scripts. Here’s how to get started.

Set Up Your Project

1. **Initialize**: Create a new project:
    ```shell
    mkdir my-app && cd my-app
    phpkg init
    ```
    - Adds Packages/` for dependencies, phpkg.config.json` for settings, and `phpkg.config-lock.json` for metadata.

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
    phpkg add https://github.com/php-repos/test-runner.git
    ```
    - Clones `test-runner` to `Packages/`, updates configs with version and hash.

    _No central repo—just Git URLs. Works with GitHub now, GitLab and others soon._

4. **Build**: Compile for development:
    ```shell
    phpkg build
    ```
   - Creates `builds/development/`, autoloads dependencies into entry points (e.g., `public/index.php`).

   _Watch changes live with `phpkg watch` or build for production with `phpkg build production`._

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
phpkg run https://github.com/php-repos/weather
```

- Outputs weather forecast in your terminal—no setup.

---

### Example: Build a Simple App

1. **Init**: `phpkg init`
2. **Add Code**:
    ```php
    // src/Hello.php
    namespace App;
    function greet($name) { return "Hello, $name!"; }
    ```
   ```php
    // public/index.php
    require 'builds/development/phpkg.imports.php';
    echo \App\greet('World');
    ```
3. **Build**: `phpkg build`
4. **Run**:
    ```shell
    cd builds/development
    php public/index.php
    ```
   _Output: “Hello, World!”_

_`phpkg` autoloads namespaced functions like `App\greet`—no classes needed for simple tasks._

---

### Why phpkg?

- **Function-First Autoloading**: `phpkg` autoloads namespaced functions—not just classes—letting you write simple, reusable functions instead of wrapping everything in objects. Unlike Composer’s class-only PSR-4, this unlocks functional programming in PHP, making your code cleaner and more expressive.
- **Speed**: Installs in seconds, builds without bloat—no heavy `vendor/` dirs or lock files slowing you down.
- **Freedom**: Use any Git repo directly—no central registry or middleman locking you in.
- **Simplicity**: Minimal setup, maximum control—focus on coding, not configuring.
