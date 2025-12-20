# Troubleshooting Guide

Common issues and solutions when working with phpkg.

---

## Installation Issues

### phpkg command not found

**Symptoms**: `phpkg: command not found` after installation

**Solutions**:
1. **Check PATH**: Verify `~/.phpkg/bin` is in your PATH:
   ```bash
   echo $PATH | grep phpkg
   ```

2. **Reload shell**: Open a new terminal or reload your shell:
   ```bash
   source ~/.bashrc  # or ~/.zshrc
   ```

3. **Manual PATH**: Add to your shell config:
   ```bash
   echo 'export PATH="$HOME/.phpkg/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ```

4. **Windows**: Ensure `%USERPROFILE%\.phpkg` is in your PATH. Restart PowerShell/CMD.

### Installation script fails

**Symptoms**: Installation script errors or hangs

**Solutions**:
- **Check internet**: Ensure you can access GitHub
- **Check permissions**: Script needs execute permissions (Unix)
- **Try manual install**: Download and run the script manually
- **Check PHP version**: Ensure PHP 8.1+ is installed and in PATH

---

## Package Management Issues

### Package not found / Invalid identifier

**Symptoms**: `❌ The given identifier is invalid.`

**Solutions**:
1. **Check format**: Use correct format:
   ```bash
   # ✅ Correct
   phpkg add php-repos/observer
   phpkg add owner/repo
   
   # ❌ Wrong
   phpkg add observer/repo/subfolder
   ```

2. **Verify repository exists**: Check the GitHub repository exists and is accessible

3. **Use full URL**: Try with full Git URL:
   ```bash
   phpkg add https://github.com/php-repos/observer.git
   ```

### Rate limit exceeded

**Symptoms**: `Rate limit exceeded` or `403 Forbidden` errors

**Solutions**:
1. **Add GitHub token**:
   ```bash
   phpkg credential github.com <your-token>
   ```

2. **Use environment variable**:
   ```bash
   export GITHUB_TOKEN=your_token_here
   ```

3. **Generate token**: Create at [GitHub Settings](https://github.com/settings/tokens)

### Package has no releases

**Symptoms**: `🔍 Could not detect any release for the given package.`

**Solutions**:
1. **Use development version**:
   ```bash
   phpkg add owner/repo --version=development
   ```
   This locks to the latest commit hash at the time of adding.

2. **Check repository**: Verify the repository has tags/releases on GitHub

3. **Create a release**: If it's your package, create a release tag

### Version not found

**Symptoms**: `Version vX.Y.Z not found`

**Solutions**:
1. **Check available versions**: Visit the repository's releases page
2. **Use exact version**: Make sure you're using the complete version number (e.g., `v1.2.3`)
3. **Use latest**: Omit `--version` to get the latest release
4. **Use development**: `--version=development` locks to the latest commit hash at the time of adding/updating

---

## Build Issues

### Build fails silently

**Symptoms**: Build completes but code doesn't work

**Solutions**:
1. **Check verbose output**:
   ```bash
   phpkg -vv build
   ```

2. **Verify entry points**: Check `phpkg.config.json` has correct entry points

3. **Check namespace mapping**: Ensure `map` in config matches your code structure

4. **Verify packages installed**: Run `phpkg install` first

### Autoloading not working

**Symptoms**: `Class not found` or `Function not found` errors

**Solutions**:
1. **Check import file**: Ensure entry point includes:
   ```php
   require 'build/phpkg.imports.php';
   ```

2. **Verify namespace mapping**: Check `phpkg.config.json`:
   ```json
   {
     "map": {
       "App": "src"  // App\ namespace → src/ directory
     }
   }
   ```

3. **Rebuild**: Run `phpkg build` after config changes

4. **Check file structure**: Ensure files match namespace structure:
   ```
   src/
     Utils.php  → namespace App\Utils;
   ```

### Build directory not found

**Symptoms**: `build/` directory doesn't exist

**Solutions**:
1. **Run build**: `phpkg build` creates the directory
2. **Check permissions**: Ensure write permissions in project directory
3. **Check config**: Verify `entry-points` are set in `phpkg.config.json`

---

## Runtime Issues

### Standalone run fails

**Symptoms**: `phpkg run` errors or doesn't execute

**Solutions**:
1. **Check entry points**: Package must have `entry-points` in `phpkg.config.json`
2. **Use verbose mode**: `phpkg -vv run package` for details
3. **Check PHP version**: Ensure PHP 8.1+ is installed
4. **Try full URL**: Use full Git URL instead of simplified format

### Serve command doesn't start

**Symptoms**: `phpkg serve` fails to start server

**Solutions**:
1. **Check port availability**: Port 8000 might be in use, try different port:
   ```bash
   phpkg serve package --port=8080
   ```

2. **Check entry points**: Package needs at least one entry point

3. **Windows**: Ensure PHP is in PATH and `php -S` works

4. **PCNTL (Unix)**: On Unix systems, PCNTL extension is required

### Watch command not detecting changes

**Symptoms**: `phpkg watch` doesn't rebuild on file changes

**Solutions**:
1. **Check file watching tools**: Install native tools:
   - **macOS**: `brew install fswatch`
   - **Linux**: `sudo apt-get install inotify-tools`
   - **Windows**: Uses polling (slower but works)

2. **Check paths**: Ensure watched files are in mapped directories

3. **Manual rebuild**: Use `phpkg build` if watch isn't working

---

## Configuration Issues

### Config file not found

**Symptoms**: `📄 Could not read the project config.`

**Solutions**:
1. **Initialize project**: Run `phpkg init` in project root
2. **Check location**: Ensure `phpkg.config.json` exists in current directory
3. **Check permissions**: Verify read permissions on config file

### Invalid JSON in config

**Symptoms**: JSON parsing errors

**Solutions**:
1. **Validate JSON**: Use a JSON validator or `php -r 'json_decode(file_get_contents("phpkg.config.json"));'`
2. **Check syntax**: Look for trailing commas, missing quotes
3. **Backup and recreate**: Backup config, run `phpkg init`, merge changes

### Packages not installing

**Symptoms**: `phpkg install` doesn't download packages

**Solutions**:
1. **Check config**: Verify `packages` section has entries
2. **Check credentials**: Private repos need GitHub token
3. **Check network**: Ensure Git access works
4. **Use verbose**: `phpkg -vv install` for details

---

## Performance Issues

### Slow builds

**Symptoms**: Builds take too long

**Solutions**:
1. **Check excludes**: Add large directories to `excludes`:
   ```json
   {
     "excludes": ["node_modules", "vendor", ".git"]
   }
   ```

2. **Add exclusions**: Exclude unnecessary files in `excludes` config

3. **Check package count**: Many packages slow builds

### High memory usage

**Symptoms**: PHP memory errors during build

**Solutions**:
1. **Increase memory**: `php -d memory_limit=512M phpkg build`
2. **Reduce packages**: Remove unused packages
3. **Check excludes**: Exclude large files/directories

---

## Git & Authentication Issues

### SSH authentication fails

**Symptoms**: Permission denied (publickey) errors

**Solutions**:
1. **Check SSH keys**: Ensure SSH key is added to GitHub
2. **Test SSH**: `ssh -T git@github.com`
3. **Use HTTPS**: Switch to HTTPS URLs instead
4. **Add token**: Use `phpkg credential` for HTTPS

### Private repository access fails

**Symptoms**: 404 Not Found for private repos

**Solutions**:
1. **Add GitHub token**:
   ```bash
   phpkg credential github.com <token>
   ```

2. **Check token permissions**: Token needs `repo` scope

3. **Use HTTPS**: Private repos work better with HTTPS + token

---

## Debugging Tips

### Enable verbose logging

Use verbose flags to see what's happening:

```bash
phpkg -v command    # Basic verbose
phpkg -vv command   # More details
phpkg -vvv command  # Maximum verbosity + debug
```

### Check logs

phpkg logs are stored in:
- **Unix/macOS**: `~/.phpkg/Logs/phpkg.log`
- **Windows**: `%USERPROFILE%\.phpkg\Logs\phpkg.log`

### Verify installation

```bash
# Check version
phpkg version

# Check PHP version
php -v

# Check Git
git --version
```

### Test package access

```bash
# Test GitHub access
curl -H "Authorization: token YOUR_TOKEN" https://api.github.com/user

# Test Git clone
git clone https://github.com/php-repos/observer.git /tmp/test
```

---

## Still Stuck?

1. **Check FAQ**: See [FAQ](https://phpkg.com/documentations/faq) for common questions
2. **Review docs**: Check relevant command documentation
3. **Enable verbose**: Use `-vvv` flag for maximum debugging
4. **Check logs**: Review log files in `~/.phpkg/Logs/`
5. **Verify versions**: Ensure PHP 8.1+, Git, and phpkg are up to date

---

## Common Error Messages

| Error | Meaning | Solution |
|-------|---------|----------|
| `❌ The given identifier is invalid.` | Package format incorrect | Use `owner/repo` or full URL |
| `🔍 Could not detect any release` | No tags in repository | Use `--version=development` to lock to latest commit hash |
| `📄 Could not read the project config.` | Missing `phpkg.config.json` | Run `phpkg init` |
| `🔑 Could not read credentials.` | Authentication needed | Add GitHub token |
| `⚠️ The package is already added` | Duplicate package | Use `update` instead of `add` |
| `📦 Could not get package` | Network/auth issue | Check credentials and network |

---

For more help, see the [FAQ](https://phpkg.com/documentations/faq) or review the [documentation index](https://phpkg.com/documentations/README).

---

## Related Documentation

- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
- **[Installation](https://phpkg.com/documentations/installation)** - Installation guide
- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command
