## Init Command

### Kickstart Your phpkg Project
Ready to manage dependencies with `phpkg`? The `init` command sets up your project in seconds, creating the foundation for autoloading functions and classes from Git repos—no Composer clutter needed.

---

### Usage
Run this in your project’s root directory:
```bash
phpkg init
```

- **What It Does**:
    - Creates `phpkg.config.json`: Configures your namespace mappings and settings.
    - Creates `phpkg.config-lock.json`: Tracks your added packages’ versions and metadata.
    - Adds a `Packages/` directory: Stores source code for packages you install.

Want a custom packages directory? Use:

```shell
phpkg init --packages-directory=vendor
```

- Renames `Packages/` to `vendor/` (or any name you pick).

---

### Next Steps

After running `init`, tweak `phpkg.config.json` to map your code (e.g., `App` → `src/`). Example:

```json
{
    "map": {"App": "src"},
    "entry-points": ["public/index.php"],
    "packages": []
}
```

Then, add packages with `phpkg add` and build with `phpkg build`. See [Customization](https://phpkg.com/documentations/customization) for details.

_One command, and you’re ready to autoload your way to cleaner PHP code._
