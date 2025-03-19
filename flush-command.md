## Flush Command

### Wipe the Slate Clean

Need a fresh start? The `phpkg flush` command clears out all files and directories created during the build process—think of it as a reset button for your `builds/` directory. Whether you’re troubleshooting, cleaning up clutter, or prepping for a new build, `flush` gets you back to square one fast.

---

### Usage

From your project’s root directory, run:

```bash
phpkg flush
```

- **What It Does**: Deletes everything in `builds/`—all environment directories like `development/` and `production/`.  
- **After**: Your `builds/` directory is empty, ready for a fresh `phpkg build`.

> Caution: This wipes all built files—back up anything you need before running it!

### Why Use It?

- **Fresh Builds**: Start over without leftover artifacts messing up your next `phpkg build`.  
- **Troubleshooting**: Clear corrupted or outdated builds to debug issues.  
- **Clean Slate**: Free up space by ditching unused environment dirs.

Check `builds/` after running—it should be empty. Then, rebuild with:

```bash
phpkg build  # or phpkg build production
```

---

### Tips

- **Backup First**: Save custom files in `builds/` (if any) before flushing—they’ll be gone.  
- **Pair with Build**: Use `flush` then `build` for a clean, reliable setup.  
- **See the Process**: Want details on builds? Check [Build Command](https://phpkg.com/documentations/build-command).
