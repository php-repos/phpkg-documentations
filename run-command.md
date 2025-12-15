# Run Command

## Unleash PHP Tools Anywhere

Imagine running a PHP tool—like a static analyzer or a weather checker—without embedding it in a project or fussing with dependencies. The `phpkg run` command makes this real: it grabs any `phpkg`-compatible Git repository, builds it on the fly, and executes it right in your terminal. No installs, no web servers—just pure PHP power at your fingertips.

- **Why It's Revolutionary**: Turns PHP into a tool-runner, not just a web engine.
- **Big Idea**: Stop bloating projects with dev tools—run them standalone, once per machine.

---

## Usage

Pass a package identifier (simplified format or full Git URL) or local path to `phpkg run`:

### From a Git URL

```bash
phpkg run <package-identifier> [entry-point]
```

### Simplified Formats

For GitHub packages, you can use the `owner/repo` format:
```bash
phpkg run php-repos/chuck-norris
phpkg run owner/repo
```

For packages in the `php-repos` organization, you can use just the repo name:
```bash
phpkg run chuck-norris
phpkg run weather
```

### Full Git URLs

- **HTTPS**:  
    ```bash
    phpkg run https://github.com/owner/repo.git
    ```
- **SSH**:  

    ```bash
    phpkg run git@github.com:owner/repo.git
    ```

### Pick an Entry Point

Multiple entry points in `phpkg.config.json`? Specify one:  

```bash
phpkg run php-repos/chuck-norris jokes.php
# or
phpkg run https://github.com/php-repos/chuck-norris.git jokes.php
```

- Default: Runs the first entry point listed.

### Set a Version

- Latest release by default. For a specific version, you must use the `--version` flag and specify an entry point:  

    ```bash
    phpkg run php-repos/weather entry.php --version=v1.2.3
    # or
    phpkg run https://github.com/php-repos/weather.git entry.php --version=v1.2.3
    ```

- Dev version with a commit (entry point required):  
    ```bash
    phpkg run php-repos/chuck-norris jokes.php --version=development#336212f42b0d612a1397e5009f2e3c681851d770
    # or
    phpkg run https://github.com/php-repos/chuck-norris.git jokes.php --version=development#336212f42b0d612a1397e5009f2e3c681851d770
    ```

> **Note**: When using `--version`, you must specify an entry point. Positional version arguments (like `phpkg run package v1.2.3`) are not supported.

### From a Local Path

Test a package on your machine:  
```bash
phpkg run ../relative/path/to/package
phpkg run /absolute/path/to/package
```

**How It Works**: Downloads (or uses local), builds in a temp sandbox, runs the entry point, and cleans up on reboot—no project changes.

---

## Why It Matters

PHP isn't just for websites—it's for tools. The `run` command breaks the mold:

- **Standalone Power**: Run analyzers (e.g., PHPStan) or utilities without project bloat.  
    ```bash
    phpkg run phpstan/phpstan phpstan analyze /path/to/project
    # or
    phpkg run https://github.com/phpstan/phpstan.git phpstan analyze /path/to/project
    ```
- **Real Apps**: Build CLI tools—like a daily dashboard—usable anywhere.  
    ```bash
    phpkg run php-repos/daily-routine
    # or
    phpkg run https://github.com/php-repos/test-runner.git
    ```
- **Efficiency**: Install once globally, not per project—less waste, faster setups.

Unlike Composer, which ties tools to `vendor/`, `phpkg run` frees them to stand alone, slashing redundancy and complexity.

## Examples

- Chuck Norris Jokes:

    ```bash
    phpkg run php-repos/chuck-norris
    # or
    phpkg run https://github.com/php-repos/chuck-norris.git
    ```

    Output: A Chuck Norris quip from https://api.chucknorris.io/.

- Weather Check:  

    ```bash
    phpkg run php-repos/weather
    # or
    phpkg run https://github.com/php-repos/weather.git
    ```
    Output: Your local forecast in the terminal.

- Static Analysis:  
    ```bash
    phpkg run phpstan/phpstan phpstan analyze ./my-app
    # or
    phpkg run https://github.com/phpstan/phpstan.git phpstan analyze ./my-app
    ```
    Output: Code analysis, no install needed.

---

## Troubleshooting

### Error: `📄 Could not read the project config.` or package not found

**Cause**: Package doesn't exist, invalid identifier, or network issue.

**Solutions**:
- Verify package identifier is correct: `owner/repo` or full URL
- Check package exists on GitHub
- Try with full URL instead of simplified format
- Use verbose mode: `phpkg -vv run package`

**Example**:
```bash
# Try with full URL
phpkg run https://github.com/php-repos/chuck-norris.git

# Or check with verbose
phpkg -vv run php-repos/chuck-norris
```

### Error: No entry points found

**Cause**: Package doesn't have `entry-points` configured in its `phpkg.config.json`.

**Solutions**:
- Check package's `phpkg.config.json` for `entry-points`
- Specify entry point manually: `phpkg run package entry.php`
- Package might not be phpkg-compatible
- Contact package maintainer

**Example**:
```bash
# Specify entry point
phpkg run package bin/console
phpkg run package public/index.php
```

### Error: Package execution fails

**Cause**: Missing dependencies, PHP version incompatibility, or package errors.

**Solutions**:
- Check PHP version: `php -v` (needs 8.1+)
- Check package requirements
- Use verbose mode: `phpkg -vvv run package`
- Check package's README for requirements

**Example**:
```bash
# Check PHP version
php -v

# Run with maximum verbosity
phpkg -vvv run package
```

### Error: Rate limit exceeded

**Cause**: GitHub API rate limits.

**Solutions**:
- Add GitHub token: `phpkg credential github.com <token>`
- Set environment variable: `export GITHUB_TOKEN=your_token`
- Wait for rate limit to reset

**Example**:
```bash
phpkg credential github.com ghp_your_token_here
phpkg run package
```

### Package downloads but doesn't execute

**Cause**: Entry point not executable or missing dependencies.

**Solutions**:
- Check entry point file exists and is readable
- Verify package has all dependencies
- Check PHP errors: `phpkg -vvv run package`
- Try specifying entry point explicitly

**Example**:
```bash
# Specify entry point
phpkg run package public/index.php

# Check for errors
phpkg -vvv run package 2>&1 | grep -i error
```

### Error: Version not found

**Cause**: Specified version doesn't exist.

**Solutions**:
- Omit `--version` to use latest
- Check available versions on GitHub
- Use exact version number with `--version` flag and entry point: `phpkg run package entry.php --version=v1.2.3` (complete version required)
- Use development version: `phpkg run package entry.php --version=development`

**Example**:
```bash
# Use latest (entry point optional)
phpkg run package

# Or use exact version (entry point required when using --version)
phpkg run package entry.php --version=v1.2.3
```

### Local path not working

**Cause**: Invalid path or missing files.

**Solutions**:
- Verify path is correct (relative or absolute)
- Check path exists: `ls -la path/to/package`
- Ensure package has `phpkg.config.json` with entry points
- Use absolute path if relative doesn't work

**Example**:
```bash
# Check path
ls -la ../relative/path

# Use absolute path
phpkg run /absolute/path/to/package
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Tokens**: GitHub rate limits? Add a token via [Credential Command](https://phpkg.com/documentations/credential-command).  
- **Entry Points**: See a package's `phpkg.config.json` for options—check [Customization](https://phpkg.com/documentations/customization).  
- **Keep It**: Want it permanent? Use `phpkg add` instead.  
- **Dream Big**: Create your own CLI tools—PHP's limits are yours to break.

---

## Related Commands

- **[Serve Command](https://phpkg.com/documentations/serve-command)** - Serve packages as web apps
- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages permanently to your project
- **[Credential Command](https://phpkg.com/documentations/credential-command)** - Manage Git credentials
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
