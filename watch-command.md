## Watch Command

### Build on the Fly

Tired of running `phpkg build` after every tweak? The `phpkg watch` command keeps your project in sync by automatically rebuilding it whenever your source files change. It’s a must-have for development—code, save, and see updates instantly.

- **Why Use It?**: Speeds up your workflow with real-time builds.
- **How It Works**: Monitors your files and triggers `build` on changes.

---

### Usage

From your project’s root directory, run:

```bash
phpkg watch
```

- **What It Does**: Watches your source files (mapped in `phpkg.config.json`) and rebuilds to `builds/development/` on any change.  
- **How to Stop**: Hit `Ctrl+C` in the terminal.

_Tip_: Pair it with your dev setup—edit, refresh, repeat.

---

### Why It’s Handy

- **Instant Feedback**: See changes without lifting a finger.  
- **Dev Flow**: Focus on coding, not rebuilding.  
- **Consistency**: Keeps `builds/development/` up-to-date with your latest work.

After starting, tweak a file—**watch** handles the rest.

---

### Tips

- Config Matters: Ensure your `phpkg.config.json` maps source dirs correctly—see [Customization](https://phpkg.com/documentations/customization).  
- Test It: Edit a file (e.g., `src/App.php`) and check `builds/development/`.  
- Next Step: Ready to deploy? Switch to `phpkg build production`—see [Build Command](https://phpkg.com/documentations/build-command).
