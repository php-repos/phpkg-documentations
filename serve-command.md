# Serve Command

## Launch PHP Apps Without a Web Server

Why limit PHP to websites? The `phpkg serve` command lets you run any `phpkg`-compatible package as a standalone web app, straight from a Git URL or local path—no project install, no domain, no hassle. It spins up a local server using PHP’s built-in `php -S`, delivering your app’s entry point right to your browser.

- **Game-Changer**: Build and share web-ready tools or dashboards, no server setup needed.
- **Vision**: Expands PHP into a versatile app platform—think beyond the web.

*Requirements*: On Unix/Linux/macOS, the [PCNTL extension](https://www.php.net/manual/en/book.pcntl.php) is required for proper signal handling. Windows is supported without PCNTL.

---

## Usage

Pass a Git URL or local path to `phpkg serve`:

### From a Git URL

```bash
phpkg serve <package-url> [entry-point]
```

- **HTTPS**:  
    ```bash
    phpkg serve https://github.com/owner/repo.git
    ```
- **SSH**:  
    ```bash
    phpkg serve git@github.com:owner/repo.git
    ```
  
### Pick an Entry Point

Multiple entry points in `phpkg.config.json`? Choose one:  
```bash
phpkg serve https://github.com/php-repos/daily-routine.git dashboard.php
```

- **Default**: Serves the first entry point listed.  
- **Must-Have**: Package needs at least one entry point—see [Customization](https://phpkg.com/documentations/customization).

### Set a Version

- Latest release by default. For a specific version, you must use the `--version` flag and specify an entry point:  

    ```bash
    phpkg serve https://github.com/php-repos/daily-routine.git dashboard.php --version=v1.0.0
    ```
- Dev version with a commit (entry point required):  
    ```bash
    phpkg serve https://github.com/php-repos/daily-routine.git dashboard.php --version=development#f2ffcee641009d753c72a935a083b2fc650787c1
    ```

> **Note**: When using `--version`, you must specify an entry point. Positional version arguments (like `phpkg serve package v1.0.0`) are not supported.

### From a Local Path

Serve a package on your machine:  

```bash
phpkg serve ../relative/path/to/package
phpkg serve /absolute/path/to/package
```

- Ideal for dev testing.

_How It Works_: Downloads (or uses local), builds in a temp sandbox, and serves via `php -S` (e.g., `localhost:8000`). Cleanup happens on OS restart—no project changes.

---

## Why It Matters

PHP can do more than web pages—and `serve` proves it:

- **Instant Apps**: Launch dashboards or tools (e.g., `daily-routine`) without Apache or Nginx.  
- **No Overhead**: Skip project dependencies—run standalone, anywhere.  
- **Creative Freedom**: Build web-accessible PHP apps for yourself or others, no domain required.

Unlike Composer’s web-only focus, `phpkg serve` turns PHP into a universal app runner.

---

## Examples

Serve the `daily-routine` package—a dashboard for your day:  

```bash
phpkg serve php-repos/daily-routine
# or
phpkg serve https://github.com/php-repos/daily-routine.git
```

- Output: Open `http://localhost:8000` to see tasks, crypto prices, news, and weather.
- No Setup: Just one command, no server config.

---

## Troubleshooting

### Error: Port already in use

**Cause**: Port 8000 (or specified port) is already occupied.

**Solutions**:
- Use different port: `phpkg serve package --port=8080`
- Find what's using the port: `lsof -i :8000` (Unix) or `netstat -ano | findstr :8000` (Windows)
- Stop the process using the port
- Use a different port number

**Example**:
```bash
# Use different port
phpkg serve package --port=8080

# Or find and stop process on port 8000
lsof -ti:8000 | xargs kill
phpkg serve package
```

### Error: No entry points found

**Cause**: Package doesn't have `entry-points` configured.

**Solutions**:
- Check package's `phpkg.config.json` for `entry-points`
- Specify entry point: `phpkg serve package entry.php`
- Package might not be phpkg-compatible
- Contact package maintainer

**Example**:
```bash
# Specify entry point
phpkg serve package public/index.php
phpkg serve package dashboard.php
```

### Error: Server starts but page doesn't load

**Cause**: Entry point path incorrect or server configuration issue.

**Solutions**:
- Check entry point file exists in package
- Verify entry point path is correct
- Check server output for errors
- Try different entry point

**Example**:
```bash
# Check package structure
phpkg serve package --port=8080
# Then check browser console and server output
```

### Error: PCNTL extension required (Unix)

**Cause**: PCNTL extension not installed (required on Unix systems).

**Solutions**:
- Install PCNTL: `sudo apt-get install php-pcntl` (Linux) or `brew install php` (macOS)
- Enable extension in `php.ini`: `extension=pcntl`
- Restart PHP/web server
- Note: Windows doesn't require PCNTL

**Example**:
```bash
# Install PCNTL (Ubuntu/Debian)
sudo apt-get install php-pcntl

# Or enable in php.ini
echo "extension=pcntl" >> /etc/php/8.1/cli/php.ini
```

### Error: Package not found or invalid identifier

**Cause**: Package identifier incorrect or package doesn't exist.

**Solutions**:
- Verify package identifier: `owner/repo` or full URL
- Check package exists on GitHub
- Try with full URL
- Use verbose mode: `phpkg -vv serve package`

**Example**:
```bash
# Try with full URL
phpkg serve https://github.com/php-repos/daily-routine.git

# Or check with verbose
phpkg -vv serve php-repos/daily-routine
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
phpkg serve package
```

### Server stops immediately

**Cause**: PHP errors in entry point or missing dependencies.

**Solutions**:
- Check server output for PHP errors
- Verify entry point is valid PHP
- Check package dependencies are met
- Use verbose mode: `phpkg -vvv serve package`

**Example**:
```bash
# Check for errors
phpkg -vvv serve package

# Look for PHP errors in output
```

### Can't access server from browser

**Cause**: Firewall, network, or host binding issue.

**Solutions**:
- Check firewall allows port
- Try `localhost` instead of `127.0.0.1`
- Verify host binding: `--host=0.0.0.0` for network access
- Check if server is actually running

**Example**:
```bash
# Bind to all interfaces
phpkg serve package --host=0.0.0.0 --port=8000

# Then access from browser
# http://your-ip:8000
```

### Windows-specific issues

**Cause**: Windows path or process handling differences.

**Solutions**:
- Use forward slashes in paths
- Check PHP is in PATH
- Verify `php -S` works: `php -S localhost:8000`
- Check Windows firewall settings

**Example**:
```bash
# Test PHP built-in server
php -S localhost:8000

# If that works, try phpkg serve
phpkg serve package
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Access**: Visit `localhost:8000` (or the port shown) in your browser.  
- **Tokens**: GitHub rate limits? Add a token via [Credential Command](https://phpkg.com/documentations/credential-command).  
- **Entry Points**: Check `phpkg.config.json` for options—see [Customization](https://phpkg.com/documentations/customization).  
- **Keep It**: Want it permanent? Use `phpkg add` instead.

---

## Related Commands

- **[Run Command](https://phpkg.com/documentations/run-command)** - Run packages as CLI tools
- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages permanently to your project
- **[Credential Command](https://phpkg.com/documentations/credential-command)** - Manage Git credentials
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works under the hood
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common issues
