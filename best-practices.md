# Best Practices

Recommended patterns and workflows for using phpkg effectively.

---

## Project Structure

### Recommended Directory Layout

```
my-project/
├── phpkg.config.json          # Configuration (commit this)
├── phpkg.config-lock.json     # Lock file (commit this)
├── Source/                     # Source code
│   └── App/
│       ├── Controllers/
│       ├── Models/
│       └── Utils/
├── Tests/                      # Test files
├── Public/                     # Entry points
│   └── index.php
├── Packages/                  # Dependencies (gitignore)
└── build/                     # Build output (gitignore)
```

### What to Commit

✅ **Commit**:
- `phpkg.config.json` - Project configuration
- `phpkg.config-lock.json` - Locked versions
- `Source/` - Source code
- `Public/` - Entry points
- `Tests/` - Test files

❌ **Don't commit**:
- `Packages/` - Dependencies (use `phpkg install`)
- `build/` - Build artifacts (regenerated)
- `phpkg.imports.php` - Auto-generated

### .gitignore Example

```gitignore
# phpkg
Packages/
build/
phpkg.imports.php

# IDE
.idea/
.vscode/
*.swp

# OS
.DS_Store
Thumbs.db
```

---

## Package Management

### Use Simplified Formats

✅ **Good**:
```bash
phpkg add php-repos/observer
phpkg add symfony/console
```

❌ **Avoid** (unless necessary):
```bash
phpkg add https://github.com/php-repos/observer.git
```

**Why**: Shorter, cleaner, easier to read and maintain.

### Version Management Strategy

#### During Development
Use latest release (omit version) or development version:
```bash
phpkg add package                    # Latest release
phpkg add package --version=development  # Latest commit
```

#### For Stable Releases
Pin to exact version numbers (complete version required):
```bash
phpkg add package v1.2.3
# or
phpkg add package --version=v1.2.3
```

**Why**: Ensures reproducible builds and prevents breaking changes.

### Use Aliases for Common Packages

```bash
# Set up aliases
phpkg alias observer https://github.com/php-repos/observer.git
phpkg alias dt https://github.com/php-repos/datatype.git

# Use them
phpkg add observer
phpkg update dt
```

**Why**: Consistency across team, easier to remember.

### Commit Lock Files

Always commit `phpkg.config-lock.json`:

```bash
git add phpkg.config.json phpkg.config-lock.json
git commit -m "Add dependencies"
```

**Why**: Ensures everyone gets the same package versions.

---

## Configuration

### Namespace Mapping Best Practices

#### Match Directory Structure

✅ **Good**:
```json
{
  "map": {
    "App": "Source",
    "App\\Controllers": "Source/Controllers",
    "App\\Models": "Source/Models"
  }
}
```

❌ **Avoid**:
```json
{
  "map": {
    "App": "Source",
    "Controllers": "Source/Controllers"  // Missing App\ prefix
  }
}
```

#### Use PSR-4 Conventions

Follow PSR-4 naming:
- Namespace matches directory structure
- One namespace per directory level
- Consistent naming across project

### Entry Points

#### Organize by Purpose

```json
{
  "entry-points": [
    "Public/index.php",      # Web app
    "cli/console.php"        # CLI tool
  ]
}
```

### Excludes

#### Exclude Development Files

```json
{
  "excludes": [
    "node_modules",
    ".git",
    "docs",
    ".idea",
    "*.md"
  ]
}
```

---

## Development Workflow

### Use Watch Mode

During development:
```bash
phpkg watch
```

**Why**: Auto-rebuilds on changes, faster feedback loop.

### Build Before Committing

```bash
phpkg build
# Test your changes
git add .
git commit
```

**Why**: Ensures build works before sharing code.

### Optimize Your Build

```bash
# Build with exclusions configured
phpkg build
```

**Why**: Use `excludes` in config to reduce build size and improve performance.

---

## Dependency Management

### Keep Dependencies Up to Date

Regularly update:
```bash
phpkg update package
```

Review changes:
```bash
git diff phpkg.config-lock.json
```

### Use Semantic Versioning

When creating packages:
- `v1.0.0` - Major release
- `v1.1.0` - Minor release (new features)
- `v1.1.1` - Patch release (bug fixes)

**Why**: Clear versioning helps users choose compatible versions.

### Document Dependencies

In your README:
```markdown
## Dependencies

- php-repos/observer (v1.0.0)
- symfony/console (v5.0.0)
```

**Why**: Helps others understand requirements.

---

## Team Collaboration

### Standardize on Aliases

Create a shared aliases file or document:

```bash
# Team aliases
phpkg alias observer https://github.com/php-repos/observer.git
phpkg alias datatype https://github.com/php-repos/datatype.git
```

**Why**: Consistency across team members.

### Use Version Control

Commit configuration files:
```bash
git add phpkg.config.json phpkg.config-lock.json
git commit -m "Add dependencies"
```

**Why**: Ensures everyone has the same setup.

### Document Setup Process

In README:
```markdown
## Setup

1. Clone repository
2. Run `phpkg install`
3. Run `phpkg build`
4. Start development server
```

**Why**: Makes onboarding easier.

---

## Performance

### Minimize Dependencies

Only add what you need:
```bash
# ✅ Good - only what's needed
phpkg add package-a
phpkg add package-b

# ❌ Avoid - unnecessary dependencies
phpkg add package-a
phpkg add package-b
phpkg add package-c  # Not used
```

**Why**: Faster builds, smaller footprint.

---

## Security

### Use Tokens for Private Repos

```bash
phpkg credential github.com <token>
```

**Why**: Secure access to private repositories.

### Don't Commit Credentials

❌ **Never commit**:
- `credentials.json`
- Tokens in config files
- API keys

✅ **Use**:
- Environment variables
- `phpkg credential` command
- CI/CD secrets

### Review Dependencies

Regularly review:
```bash
phpkg update package
```

Check for security updates.

---

## Deployment

### Build Before Deploying

```bash
phpkg build
```

**Why**: Ensures all dependencies are included and autoloading is set up.

### Verify Builds

Before deploying:
```bash
phpkg build
# Test the build
cd build
php Public/index.php
```

**Why**: Catches issues before deployment.

### Use CI/CD

Example GitHub Actions:
```yaml
- name: Install phpkg
  run: bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"

- name: Install dependencies
  run: phpkg install

- name: Build
  run: phpkg build

- name: Test
  run: php Tests/run.php
```

**Why**: Automated, consistent deployments.

---

## Package Creation

### Structure Your Package

```
my-package/
├── phpkg.config.json
├── Source/
│   └── Package/
│       └── Functions.php
├── README.md
└── LICENSE
```

### Use Semantic Versioning

Tag releases:
```bash
git tag v1.0.0
git push --tags
```

**Why**: Clear versioning for users.

### Document Your Package

In README:
- Installation instructions
- Usage examples
- API documentation
- Requirements

**Why**: Helps others use your package.

---

## Common Mistakes to Avoid

### ❌ Don't Edit Lock File Manually

Let phpkg manage it:
```bash
phpkg add package  # Updates lock file automatically
```

### ❌ Don't Commit Packages Directory

Use `.gitignore`:
```gitignore
Packages/
```

### ❌ Don't Skip Build Step

Always build after changes:
```bash
phpkg build
```

### ❌ Don't Use Development Versions for Stable Releases

Development versions lock to a specific commit hash, but that commit can change when you update. For stable releases, pin to a tagged version:

```bash
phpkg add package --version=v1.2.3
```

**Note**: When you use `--version=development`, phpkg locks to the latest commit hash at that moment. Updating with `development` moves to the newest commit hash, which may introduce breaking changes.

---

## Summary

1. ✅ Use simplified package formats
2. ✅ Commit config and lock files
3. ✅ Pin versions for stable releases
4. ✅ Use watch mode during active development
5. ✅ Exclude unnecessary files
6. ✅ Organize code with namespaces
7. ✅ Leverage function autoloading
8. ✅ Build before deploying
9. ✅ Document your setup
10. ✅ Keep dependencies updated

Following these practices will make your phpkg projects more maintainable, performant, and easier to collaborate on.

---

---

## Related Documentation

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understanding how phpkg works under the hood
- **[Customization](https://phpkg.com/documentations/customization)** - Configure your phpkg project
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
