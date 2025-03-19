## Customization

### Shape Your phpkg Project

The `phpkg init` command creates a `phpkg.config.json` file—your key to tailoring `phpkg` for your project. From mapping namespaces to autoloading functions or setting entry points, this file lets you control how `phpkg` builds and runs your code. Here’s how to make it yours.

---

### What’s in the Config?

Run `phpkg init`, and you’ll get a `phpkg.config.json` like this:

```json
{
    "map": [],
    "autoloads": [],
    "excludes": [],
    "entry-points": [],
    "executables": [],
    "import-file": "phpkg.imports.php",
    "packages-directory": "Packages",
    "packages": []
}
```

Let’s break down each part.

#### Map

Map namespaces to directories—like `App` to `src/`—so `phpkg` knows where your code lives. Example:

```json
{
    "map": {
        "App": "src",
        "Tests": "tests"
    }
}
```

- Add as many mappings as you need—`phpkg` resolves them for you.  
- Follow [PSR-4](https://www.php-fig.org/psr/psr-4/) naming for classes and functions.

##### Classes:

```php
// src/User.php
namespace App;
class User {
    // Your code
}
```

##### Functions:

```php
// src/Utils.php
namespace App\Utils;
function log($msg) { echo $msg; }
```

_Why it rocks: `phpkg` autoloads both, letting you mix OOP and functional code effortlessly._

#### Autoloads

List files to load before anything else—perfect for helpers or constants. Example:

```json
{
    "autoloads": ["src/helpers.php"]
}
```

- Add multiple files as needed.  
- Use this for utilities you want globally available, like:
    ```php
    // src/helpers.php
    function debug($var) { var_dump($var); }
    ```

#### Excludes

Skip files or dirs during builds—like `node_modules` or dev scripts. Example:

```json
{
    "excludes": ["node_modules", "build.sh"]
}
```

- Paths are relative to your project root.  
- Keeps your builds lean by ignoring runtime-irrelevant stuff.

#### Entry Points

Define where your app starts—`phpkg` adds autoloading magic here. Example:

```json
{
    "entry-points": ["public/index.php", "cli/run.php"]
}
```

- List all entry files (e.g., web or CLI).  
- `phpkg` injects imports so `App\Utils\log()` just works.

#### Executables

Turn package scripts into root-level commands via symlinks. Example:

```json
{
    "executables": {
        "rocket": "Packages/rocket/launch.php"
    }
}
```

- Run `php rocket` to execute `launch.php`.  
- Add more: `"status": "Packages/rocket/status.php"`.  
- Paths are relative to root; scripts inherit their package’s autoloads.

#### Import File

Set where `phpkg` writes import statements (default: `phpkg.imports.php`). Change it with:

```json
{
    "import-file": "vendor/autoload.php"
}
```

- Matches your project’s style—e.g., mimic Composer if you like.

#### Packages Directory

Choose where packages live (default: `Packages`). Customize it:

```json
{
    "packages-directory": "vendor"
}
```

- `phpkg add` uses this dir; builds pull from here too.  
- Add it to `.gitignore` to keep Git clean.
> Note: If it doesn’t exist, `phpkg` creates it.

#### Packages

Tracks installed packages—`phpkg` fills this automatically with `add`, `update`, or `remove`. Example:

```json
{
    "packages": {
        "https://github.com/php-repos/test-runner.git": "1.0.0",
        "https://github.com/php-repos/datatype.git": "2.5.0"
    }
}
```

Lists Git URLs and versions—no manual edits needed.

---

### Get Started

Edit `phpkg.config.json` after `phpkg init`, then use `phpkg build` to see it in action. Need more? Check [Init Command](https://phpkg.com/documentations/init-command) or dive into other commands like `phpkg add`.
