# Flush Command

## Wipe the Slate Clean

Need a fresh start? The `phpkg flush` command clears out all files and directories created during the build process—think of it as a reset button for your `build/` directory. It also clears phpkg's package caches stored in a temporary directory. Whether you're troubleshooting, cleaning up clutter, or prepping for a new build, `flush` gets you back to square one fast.

## Usage

From your project's root directory, run:

```bash
phpkg flush
```

- **What It Does**: 
  - Deletes everything in `build/` directory
  - Clears phpkg's package caches (downloaded packages stored in temp directory)
- **After**: Your `build/` directory is empty and caches are cleared, ready for a fresh `phpkg build`.

> Caution: This wipes all built files—back up anything you need before running it!

## Why Use It?

- **Fresh Builds**: Start over without leftover artifacts messing up your next `phpkg build`.  
- **Troubleshooting**: Clear corrupted or outdated builds to debug issues.  
- **Clean Slate**: Free up space by removing build directory.
- **Clear Caches**: Remove cached package downloads to force re-downloading if a download is broken or corrupted. phpkg caches downloaded packages in a temp directory to reduce downloads for the same package across different projects.

Check `build/` after running—it should be empty. Then, rebuild with:

```bash
phpkg build
```

---

## Common Use Cases

### Clean Rebuild
```bash
phpkg flush
phpkg build
```

### Troubleshooting Build Issues
```bash
phpkg flush
phpkg build
# Test if issues are resolved
```

### Fix Broken Package Downloads
If a package download is corrupted or broken, flush clears the cache to force a fresh download:
```bash
phpkg flush
phpkg install  # or phpkg add/update
# Packages will be re-downloaded from scratch
```

### Before Fresh Build
```bash
phpkg flush
phpkg build
```

## Tips

- **Backup First**: Save custom files in `build/` (if any) before flushing—they'll be gone.  
- **Pair with Build**: Use `flush` then `build` for a clean, reliable setup.  
- **CI/CD**: Useful in automated pipelines to ensure clean builds

---

## Related Commands

- **[Build Command](https://phpkg.com/documentations/build-command)** - Build your project after flushing
- **[Watch Command](https://phpkg.com/documentations/watch-command)** - Auto-rebuild on file changes
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Build Command](https://phpkg.com/documentations/build-command)** - Learn how to build your project
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve common build issues
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Recommended workflows and patterns
