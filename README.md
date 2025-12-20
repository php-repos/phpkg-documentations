# phpkg

## A package manager to boost your code

**phpkg** is a modern PHP package manager that brings Git-based dependency management to PHP with function-first autoloading. We've brought back all PHP functionalities for you so you can write code however you want.

---

## phpkg is more than a package manager

We've created a tool that has everything you need to build rapid applications.

### Functional and OOP
It supports both functional and OOP programming! Autoload namespaced functions alongside classes—no class wrappers needed.

### No Intermediate Repo
It uses Git packages directly from repository URLs. No central registry, no middleman—just direct Git access.

### JIT Compile
It only requires used files to your project, not all of them! Builds are optimized and lean.

---

## Quick Start

```bash
# Install phpkg
bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"

# Try it out
phpkg run php-repos/chuck-norris

# Start a project
mkdir my-app && cd my-app
phpkg init
phpkg add php-repos/observer
phpkg build
```

**New to phpkg?** Start with the [Getting Started Guide](https://phpkg.com/documentations/getting-started).

---

## Documentation Index

### 🚀 Getting Started
- **[Installation](https://phpkg.com/documentations/installation)** - Install phpkg on your system
- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Your first project with phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understanding how phpkg works

### 📦 Core Commands

#### Package Management
- **[Add](https://phpkg.com/documentations/add-command)** - Add packages to your project
- **[Remove](https://phpkg.com/documentations/remove-command)** - Remove packages from your project
- **[Update](https://phpkg.com/documentations/update-command)** - Update packages to new versions
- **[Install](https://phpkg.com/documentations/install-command)** - Install packages from config

#### Project Management
- **[Init](https://phpkg.com/documentations/init-command)** - Initialize a new phpkg project
- **[Build](https://phpkg.com/documentations/build-command)** - Build your project with production-ready files
- **[Watch](https://phpkg.com/documentations/watch-command)** - Auto-rebuild on file changes
- **[Flush](https://phpkg.com/documentations/flush-command)** - Clean build artifacts

#### Standalone Execution
- **[Run](https://phpkg.com/documentations/run-command)** - Run packages as CLI tools without installation
- **[Serve](https://phpkg.com/documentations/serve-command)** - Serve packages as web apps

#### Utilities
- **[Version](https://phpkg.com/documentations/version-command)** - Display phpkg version information
- **[Alias](https://phpkg.com/documentations/alias-command)** - Create shortcuts for package URLs
- **[Credential](https://phpkg.com/documentations/credential-command)** - Manage Git credentials
- **[Migrate](https://phpkg.com/documentations/migrate-command)** - Migrate from Composer

### ⚙️ Configuration & Customization
- **[Customization](https://phpkg.com/documentations/customization)** - Configure phpkg.config.json
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns

### 🆘 Help & Reference
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

---

## Why This Matters?

We believe that PHP has enormous untapped potential, and we are dedicated to creating tools that empower developers to harness its full power and capabilities. phpkg unlocks this potential by simplifying the process of using PHP to its fullest extent. With phpkg, developers can take advantage of all that PHP has to offer and build more efficient, scalable, and powerful applications.

---

## What Makes phpkg Different?

| Feature | phpkg | Composer |
|--------|-------|----------|
| Function autoloading | ✅ Yes | ❌ No |
| Git-based | ✅ Direct | ⚠️ Via Packagist |
| Central registry | ❌ No | ✅ Required |
| Standalone execution | ✅ Yes | ❌ No |
| Web app serving | ✅ Yes | ❌ No |
| Build system | ✅ Built-in | ❌ External tools |

---

## Platform Support

- ✅ **macOS** - Fully supported
- ✅ **Linux** - Fully supported  
- ✅ **Windows** - Supported (PHP 8.5+ required, fully tested; later versions may need additional testing)

---

## Next Steps

1. **[Install phpkg](https://phpkg.com/documentations/installation)** on your system
2. **[Follow the Getting Started guide](https://phpkg.com/documentations/getting-started)** to create your first project
3. **[Explore the commands](https://phpkg.com/documentations/add-command)** to understand what phpkg can do
4. **[Read Best Practices](https://phpkg.com/documentations/best-practices)** for recommended workflows

---

## Need Help?

- **Stuck?** Check the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting)
- **Questions?** See the [FAQ](https://phpkg.com/documentations/faq)
- **Best practices?** Read [Best Practices](https://phpkg.com/documentations/best-practices)

---

Happy coding with phpkg! 🚀
