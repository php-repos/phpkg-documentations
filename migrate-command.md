## Migrate Command

### Switch from Composer with Ease

If your application or package currently relies on Composer, the `phpkg migrate` command simplifies the shift to `phpkg`. It scans your `composer.json`, generates a `phpkg.config.json` with the key details, and prepares your project to leverage `phpkg`’s powerful autoloading—no tedious manual configuration required.

- **Why Migrate?**: Unlock autoloading for functions (not just classes) and embrace a streamlined, Git-based workflow.
- **What It Does**: Transforms your Composer setup into a `phpkg`-ready configuration.

---

### Usage

In the root directory of your package or application, run:

```bash
phpkg migrate
```

- **What Happens**:  
    - Reads your `composer.json` file.  
    - Creates a `phpkg.config.json` file with namespace mappings and package info.  
    - Sets your project up for `phpkg`’s build process.

**Next Step: Run `phpkg build` to autoload your code and dependencies.**

---

### Why Use It?

- **Quick Transition**: Avoid manual setup—`migrate` does the heavy lifting.  
- **Enhanced Flexibility**: Use namespaced functions alongside classes.  
- **Git-Driven Workflow**: Manage packages directly from Git repositories.

After migration, you can tweak `phpkg.config.json` as needed—see [Customization](https://phpkg.com/documentations/customization) for more.

---

### Example

Imagine your `composer.json` looks like this:

```json
{
      "autoload": {
          "psr-4": {
              "MyApp\\": "src/"
          }
      },
      "require": {
          "vendor/package": "^2.0"
      }
}
```

Running `phpkg migrate` might produce a `phpkg.config.json` like:

```json
{
      "map": {
          "MyApp": "src"
      },
      "packages": {
          "https://github.com/vendor/package.git": "^2.0"
      }
}
```

> Heads Up: Package URLs are placeholders—update them with real Git repository URLs.

Then, run `phpkg build` to get your project up and running.

---

### Tips

- **Check the Config**: Review `phpkg.config.json` post-migration to adjust settings or add entry points.  
- **Install Packages**: Use `phpkg add` to fetch packages from Git after migration.  
- **Learn More**: Visit [Build Command](https://phpkg.com/documentations/build-command) for the next steps.
