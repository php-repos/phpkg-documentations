# Watch Command

## Build on the Fly

Tired of running `phpkg build` after every tweak? The `phpkg watch` command keeps your project in sync by automatically rebuilding it whenever your source files change. It's a must-have for development—code, save, and see updates instantly.

- **Why Use It?**: Speeds up your workflow with real-time builds.
- **How It Works**: Monitors your files and triggers `build` on changes.

## Usage

From your project’s root directory, run:

```bash
phpkg watch
```

- **What It Does**: Watches your source files (mapped in `phpkg.config.json`) and rebuilds to `build/` directory on any change.  
- **How to Stop**: Hit `Ctrl+C` in the terminal.

_Tip_: Pair it with your dev setup—edit, refresh, repeat.

---

## Why It's Handy

- **Instant Feedback**: See changes without lifting a finger.  
- **Dev Flow**: Focus on coding, not rebuilding.  
- **Consistency**: Keeps `build/` directory up-to-date with your latest work.

After starting, tweak a file—**watch** handles the rest.

---

## Troubleshooting

### Watch not detecting file changes

**Cause**: File watching tools not installed or using polling mode.

**Solutions**:
- **macOS**: Install fswatch: `brew install fswatch`
- **Linux**: Install inotify-tools: `sudo apt-get install inotify-tools`
- **Windows**: Uses polling (slower but works automatically)
- Check if native tools are available: `which fswatch` or `which inotifywait`

**Example**:
```bash
# macOS
brew install fswatch

# Linux (Ubuntu/Debian)
sudo apt-get install inotify-tools

# Then try again
phpkg watch
```

### Watch using polling (slow)

**Cause**: Native file watching tools not available.

**Solutions**:
- Install native tools (see above)
- Increase wait time: `phpkg watch --wait=5` (default is 2 seconds)
- Accept slower polling if native tools unavailable

**Example**:
```bash
# Increase polling interval
phpkg watch --wait=5
```

### Error: `📄 Could not read the project config.`

**Cause**: Missing or invalid `phpkg.config.json`.

**Solutions**:
- Run `phpkg init` to create config file
- Check if you're in project root directory
- Verify `phpkg.config.json` exists and is valid JSON

**Example**:
```bash
# Initialize if missing
phpkg init
phpkg watch
```

### Build fails on every change

**Cause**: Build errors in project code or configuration.

**Solutions**:
- Fix build errors first: `phpkg build` (without watch)
- Check `phpkg.config.json` for errors
- Verify namespace mappings are correct
- Check for syntax errors in source files

**Example**:
```bash
# Test build first
phpkg build

# If successful, then watch
phpkg watch
```

### Watch stops unexpectedly

**Cause**: Process killed, errors, or system issues.

**Solutions**:
- Check for error messages in output
- Verify PHP process isn't being killed
- Check system logs
- Restart watch: `phpkg watch`

**Example**:
```bash
# Check for errors
phpkg watch 2>&1 | tee watch.log

# Review log for issues
cat watch.log
```

### Too many rebuilds (rebuilds on every keystroke)

**Cause**: Watching too many files or editor creating temp files.

**Solutions**:
- Add exclusions to `excludes` in config
- Exclude editor temp files: `*.swp`, `*.tmp`, `.idea/`
- Increase wait time: `phpkg watch --wait=3`
- Check what's being watched

**Example**:
```json
{
  "excludes": [
    "*.swp",
    "*.tmp",
    ".idea/",
    ".vscode/"
  ]
}
```

### High CPU usage

**Cause**: Too many files being watched or frequent rebuilds.

**Solutions**:
- Add more exclusions to reduce watched files
- Increase wait time for polling mode
- Exclude large directories: `node_modules/`, `.git/`
- Use native file watching tools instead of polling

**Example**:
```json
{
  "excludes": [
    "node_modules",
    ".git",
    "vendor",
    "builds"
  ]
}
```

### Watch doesn't rebuild on save

**Cause**: Files not in watched directories or excluded.

**Solutions**:
- Check `map` in config includes your source directories
- Verify files aren't in `excludes`
- Check file permissions
- Try manual build to verify it works

**Example**:
```bash
# Check config
cat phpkg.config.json

# Verify map includes your directories
# Then test manual build
phpkg build
```

For more troubleshooting help, see the [Troubleshooting Guide](https://phpkg.com/documentations/troubleshooting).

---

## Tips

- **Config Matters**: Ensure your `phpkg.config.json` maps source dirs correctly—see [Customization](https://phpkg.com/documentations/customization).  
- **Test It**: Edit a file (e.g., `src/App.php`) and check `build/` directory.  
- **Next Step**: Ready to deploy? Run `phpkg build` to create your build—see [Build Command](https://phpkg.com/documentations/build-command).

---

## Related Commands

- **[Build Command](https://phpkg.com/documentations/build-command)** - Manual build without watching
- **[Flush Command](https://phpkg.com/documentations/flush-command)** - Clean build artifacts
- **[Customization](https://phpkg.com/documentations/customization)** - Configure what files to watch
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Build Command](https://phpkg.com/documentations/build-command)** - Learn how builds work
- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Complete walkthrough of phpkg
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
