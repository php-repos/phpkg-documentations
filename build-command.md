# Build Command

## Let phpkg Handle the Heavy Lifting

Writing PHP often means wrestling with `require`, `include`, `require_once`, or `include_once` statements to load your files. It's tedious, error-prone, and a nightmare when file locations change. The `phpkg build` command eliminates this hassle by automatically resolving and injecting dependencies based on your namespace usage—whether they're classes, functions, or constants from your project or external packages. Focus on coding; `phpkg` handles the rest.

- **Winning Feature**: Autoloads namespaced functions and classes—no manual imports needed.  
- **Functional Freedom**: Write simple functions or full-blown OOP—**phpkg** supports both seamlessly.

## Usage

The `build` command creates a production-ready copy of your project.

```bash
phpkg build
```

- Outputs to `build/` directory with production-ready files.
- Uses settings from `phpkg.config.json`.
- Copies source files, packages, and generates autoloading.

> Note
> Customize your build with `phpkg.config.json`. Check the [Customization Documentation](https://phpkg.com/documentations/customization) for details.

---

### How It Works

The `build` command scans your code for namespace usage—classes, functions, and constants—and handles them differently:

- **Functions and Constants**: Adds `require_once` statements directly in the files where they are used, ensuring they're loaded when needed.
- **Classes**: Sets up autoloading in the import file (`phpkg.imports.php`) which is included in your entry points (e.g., `public/index.php`), so PHP knows where to find your classes.

Whether you're using local files or external packages, `phpkg` resolves everything based on your configuration.

### Example 1: Simple Namespace Usage

Suppose your `phpkg.config.json` maps `"Application": "src"` and sets `public/index.php` as the entry point. Here's a file at `src/ClassBar.php`:

```php
<?php

namespace Application;

use Application\SubDomain\ClassFoo;
use Exception;
use function Application\Str\between;
use const Application\Constants\CONSTANT_A;

class ClassBar extends ClassFoo {
    // Your code
}
```

After running `phpkg build`, the output becomes:

```php
<?php

namespace Application;

require_once '/var/www/src/Constants.php';  // For CONSTANT_A
require_once '/var/www/src/Str.php';       // For between()

use Application\SubDomain\ClassFoo;
use Exception;
use function Application\Str\between;
use const Application\Constants\CONSTANT_A;

class ClassBar extends ClassFoo {
    // Your code
}
```

- `require_once` statements are added directly in this file for the function `between()` and constant `CONSTANT_A`.  
- Autoloading for `ClassFoo` is configured in the import file (`phpkg.imports.php`) which is included in `public/index.php`.

### Example 2: Complex Imports with Packages

Now, consider a more intricate scenario at `src/SubDomain/ClassBar.php`:

```php
<?php

namespace Application\SubDomain;

use Application\SubDomain\ClassFoo;
use Application\AnotherNamespace\ClassBaz as Baz;
use function Application\SampleFile\anImportantFunction;
use function Application\HelperNamespace\helper1 as anotherFunction;
use const Application\Constants\CONSTANT;
use const Application\OtherConstants\RENAME as AnotherConstant;
use PackageFoo\ClassInFoo as AnotherFile, PackageBar\SubDirectory\ClassInBar;
use PackageBaz\SubDirectory\{ClassInBaz, AnotherClassInBaz as Another};
use function PackageFoo\SubDirectory\Helper\{helper1 as anotherFunction, helper2};
use const PackageBar\SubDirectory\Constants\{CONSTANT, RENAME as AnotherConstant};

class ClassBar extends ClassFoo {
    // Your code
}
```

After `phpkg build`, it transforms into:

```php
<?php

namespace Application\SubDomain;

require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Constants.php';
require_once '/var/www/src/Constants.php';
require_once '/var/www/src/OtherConstants.php';
require_once '/var/www/Packages/owner-foo/package-foo/src/SubDirectory/Helper.php';
require_once '/var/www/src/SampleFile.php';
require_once '/var/www/src/Helper.php';

use Application\SubDomain\ClassFoo;
use Application\AnotherNamespace\ClassBaz as Baz;
use function Application\SampleFile\anImportantFunction;
use function Application\HelperNamespace\helper1 as anotherFunction;
use const Application\Constants\CONSTANT;
use const Application\OtherConstants\RENAME as AnotherConstant;
use PackageFoo\ClassInFoo as AnotherFile, PackageBar\SubDirectory\ClassInBar;
use PackageBaz\SubDirectory\{ClassInBaz, AnotherClassInBaz as Another};
use function PackageFoo\SubDirectory\Helper\{helper1 as anotherFunction, helper2};
use const PackageBar\SubDirectory\Constants\{CONSTANT, RENAME as AnotherConstant};

class ClassBar extends ClassFoo {
    // Your code
}
```

- `require_once` statements are added directly in this file for all used functions and constants, including those from external packages.  
- Class autoloading is handled in the import file (`phpkg.imports.php`) which is included in `public/index.php`.

---

## Why It's a Game-Changer

- **No Manual Imports**: Stop chasing file paths—`phpkg` resolves them automatically.  
- **Functional + OOP**: Namespaced functions and classes autoload effortlessly.  
- **Refactor Freely**: Move files or directories; `phpkg` adjusts on the next build.  
- **Package Integration**: External packages work out of the box, no extra setup.

With `phpkg`, you write code—nothing else. It's a superpower for productivity.

---

## Troubleshooting

### Error: `📄 Could not read the project config.`

**Cause**: Missing or invalid `phpkg.config.json`.

**Solutions**:
- Run `phpkg init` to create config file
- Check if you're in project root directory
- Verify `phpkg.config.json` exists and is valid JSON
- Check file permissions

**Example**:
```bash
# Initialize if missing
phpkg init

# Validate JSON
php -r 'json_decode(file_get_contents("phpkg.config.json"));'
```

### Error: Classes or functions not found after build

**Cause**: Namespace mappings incorrect or entry points not configured.

**Solutions**:
- Check `map` in `phpkg.config.json` matches your directory structure
- Verify entry points are set: `"entry-points": ["public/index.php"]`
- Ensure entry points include autoload file: `require 'build/phpkg.imports.php'`
- Check file structure matches namespace declarations

**Example**:
```json
{
  "map": {
    "App": "src"  // App\ namespace → src/ directory
  },
  "entry-points": ["public/index.php"]
}
```

### Build directory not created

**Cause**: Write permissions issue or invalid config.

**Solutions**:
- Check write permissions in project directory
- Verify `entry-points` are set in config
- Ensure `packages-directory` exists or can be created
- Try with verbose mode: `phpkg -vv build`

**Example**:
```bash
# Check permissions
ls -ld .

# Fix if needed
chmod 755 .

phpkg build
```

### Build succeeds but autoloading doesn't work

**Cause**: Entry points not including autoload file or wrong path.

**Solutions**:
- Verify entry points include: `require 'build/phpkg.imports.php'`
- Check path is correct relative to entry point location
- Ensure `import-file` name matches in config
- Rebuild: `phpkg flush && phpkg build`

### Packages not included in build

**Cause**: Packages not installed or lock file missing.

**Solutions**:
- Run `phpkg install` to install packages from config
- Check `phpkg.config-lock.json` exists
- Verify packages are listed in `phpkg.config.json`
- Reinstall: `phpkg install`

**Example**:
```bash
phpkg install  # Install packages first
phpkg build    # Then build
```

### Build is slow

**Cause**: Too many files or large directories included.

**Solutions**:
- Add exclusions to `excludes` in config
- Exclude `node_modules`, `.git`, etc.
- Check what's being copied with verbose mode

**Example**:
```json
{
  "excludes": [
    "node_modules",
    ".git",
    "docs"
  ]
}
```

### Memory errors during build

**Cause**: PHP memory limit too low for large projects.

**Solutions**:
- Increase memory limit: `php -d memory_limit=512M phpkg build`
- Reduce packages or files being built
- Add more exclusions

**Example**:
```bash
php -d memory_limit=512M phpkg build
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Active Development**: Pair with `phpkg watch` to rebuild automatically on changes.  
- **Fine-Tune**: Adjust `map`, `excludes`, and more in `phpkg.config.json`—see [Customization](https://phpkg.com/documentations/customization).  
- **Troubleshooting**: Missing imports? Double-check your namespace mappings in `phpkg.config.json`.

---

## Related Commands

- **[Watch Command](https://phpkg.com/documentations/watch-command)** - Auto-rebuild on file changes
- **[Flush Command](https://phpkg.com/documentations/flush-command)** - Clean build artifacts before rebuilding
- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages before building
- **[Install Command](https://phpkg.com/documentations/install-command)** - Install packages before building
- **[Customization](https://phpkg.com/documentations/customization)** - Configure build settings
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
