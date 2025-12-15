# Installation

## Get phpkg Up and Running
Install `phpkg` and start managing PHP packages the lightweight way—no Composer bloat, just direct Git power. It sets up in your home directory, making it accessible from any project with a single command.

---

## Requirements
Ensure your system has:
- **PHP >= 8.1**: With `php-mbstring` (for string handling), `php-zip` (for unpacking archives), and `php-curl` (for Git downloads).
- **Git**: To clone repositories directly.
- **unzip**: To extract package files.

*Works on Unix/Linux/macOS and Windows. Windows users need PHP 8.5 or later (PHP 8.5 is fully tested; later versions may need additional testing).*

---

## Install in One Step

### Unix/Linux/macOS
Run this command to install `phpkg`:
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.sh)"
```

- **What It Does**: Downloads `phpkg` to `~/.phpkg`, adds it to your `$PATH` (via `.bashrc` or `.zshrc`), and preps it for use.
- **Next**: Open a new terminal to access phpkg commands—or source your current shell manually:
    ```bash
    source ~/.bashrc  # or ~/.zshrc, depending on your shell
    ```
Trouble? Verify `$PATH` includes `~/.phpkg/bin` with `echo $PATH`.

### Windows
Run this command in PowerShell to install `phpkg`:
```powershell
powershell -ExecutionPolicy Bypass -Command "Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/php-repos/phpkg-installation/master/install.ps1' -OutFile install.ps1 -UseBasicParsing; powershell -ExecutionPolicy Bypass -File install.ps1"
```

- **What It Does**: Downloads `phpkg` to `%USERPROFILE%\.phpkg`, adds it to your `PATH`, and preps it for use.
- **Next**: Open a new terminal to access phpkg commands. The PATH is updated automatically.

---

## Verify It Works

Test your install:
```bash
phpkg version
```

You should see the `phpkg` version number. Ready? Jump to [Getting Started](https://phpkg.com/documentations/getting-started) to add packages or run scripts!

## Verbose Mode

You can enable verbose logging using `-v`, `-vv`, or `-vvv` flags **before** the main command:

```bash
phpkg -v add package
phpkg -vv add package
phpkg -vvv add package
```

- **Important**: Verbose flags must come **before** the command. `phpkg add -vv package` will not work—anything after the command goes to the command itself.
- **Levels**: `-v` shows basic verbose output, `-vv` shows more details, `-vvv` shows maximum verbosity including debug information.

---

## Related Documentation

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Your first project with phpkg
- **[Version Command](https://phpkg.com/documentations/version-command)** - Check your phpkg version
- **[Concepts](https://phpkg.com/documentations/concepts)** - Understand how phpkg works
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve installation issues
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
