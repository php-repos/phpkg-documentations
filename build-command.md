## Build Command

**Let phpkg Handle the Heavy Lifting**

Writing PHP often means wrestling with `require`, `include`, `require_once`, or `include_once` statements to load your files. It’s tedious, error-prone, and a nightmare when file locations change. The `phpkg build` command eliminates this hassle by automatically resolving and injecting dependencies based on your namespace usage—whether they’re classes, functions, or constants from your project or external packages. Focus on coding; `phpkg` handles the rest.

- **Winning Feature**: Autoloads namespaced functions and classes—no manual imports needed.  
- **Functional Freedom**: Write simple functions or full-blown OOP—**phpkg** supports both seamlessly.

### Usage

The `build` command creates a ready-to-run copy of your project tailored to a specific environment.

#### Development Build

For coding and testing:
```bash
phpkg build
```

- Outputs to `builds/development/`.
- Uses settings from `phpkg.config.json`.

#### Production Build

For deployment:

```bash
phpkg build production
```

- Outputs to `builds/production/`.  
- Optimized for performance.

> Note
> Customize your build with `phpkg.config.json`. Check the [Customization Documentation](https://phpkg.com/documentations/customization) for details.

---

#### How It Works

The `build` command scans your code for namespace usage—classes, functions, and constants—and intelligently adds the necessary `require_once` statements. It also sets up autoloading in your entry points (e.g., `public/index.php`) so PHP knows where to find your classes. Whether you’re using local files or external packages, `phpkg` resolves everything based on your configuration.

#### Example 1: Simple Namespace Usage

Suppose your `phpkg.config.json` maps `"Application": "src"` and sets `public/index.php` as the entry point. Here’s a file at `src/ClassBar.php`:

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

- `require_once` statements are added for the function `between()` and constant `CONSTANT_A`.  
- Autoloading for `ClassFoo` is configured in `public/index.php`.

#### Example 2: Complex Imports with Packages

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

- `require_once` statements resolve all used functions and constants, including those from external packages.  
- Class autoloading is handled in `public/index.php`.

---

### Why It’s a Game-Changer

- **No Manual Imports**: Stop chasing file paths—`phpkg` resolves them automatically.  
- **Functional + OOP**: Namespaced functions and classes autoload effortlessly.  
- **Refactor Freely**: Move files or directories; `phpkg` adjusts on the next build.  
- **Package Integration**: External packages work out of the box, no extra setup.

With `phpkg`, you write code—nothing else. It’s a superpower for productivity.

---

### Tips

- **Development Workflow**: Pair with `phpkg watch` to rebuild automatically on changes.  
- **Production Ready**: Use `phpkg build production` for a lean, optimized output.  
- **Fine-Tune**: Adjust `map`, `excludes`, and more in `phpkg.config.json`—see [Customization](https://phpkg.com/documentations/customization).  
- **Troubleshooting**: Missing imports? Double-check your namespace mappings in `phpkg.config.json`.

---

Ready to simplify your PHP projects? Start with [Getting Started](https://phpkg.com/documentations/getting-started) or explore the [Watch Command](https://phpkg.com/documentations/watch-command) for live development.
