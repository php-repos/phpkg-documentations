## Installation

### Get phpkg Up and Running
Install `phpkg` and start managing PHP packages the lightweight way—no Composer bloat, just direct Git power. It sets up in your home directory, making it accessible from any project with a single command.

---

### Requirements
Ensure your system has:
- **PHP >= 8.1**: With `php-mbstring` (for string handling), `php-zip` (for unpacking archives), and `php-curl` (for Git downloads).
- **Git**: To clone repositories directly.
- **unzip**: To extract package files.

*Works on Unix/Linux/macOS—Windows support coming soon.*

---

### Install in One Step
Run this command to install `phpkg`:
```bash
bash -c "$(curl -fsSL https://raw.github.com/php-repos/phpkg-installation/master/install.sh)"
```

- **What It Does**: Downloads `phpkg` to `~/.phpkg`, adds it to your `$PATH` (via `.bashrc` or `.zshrc`), and preps it for use.
- **Next**: Open a new terminal to access phpkg commands—or source your current shell manually:
    ```bash
    source ~/.bashrc  # or ~/.zshrc, depending on your shell
    ```
Trouble? Verify `$PATH` includes `~/.phpkg/bin` with `echo $PATH`.

---

### Verify It Works

Test your install:
```bash
phpkg --version
```

You should see the `phpkg` version number. Ready? Jump to [Getting Started](https://phpkg.com/documentations/getting-started) to add packages or run scripts!