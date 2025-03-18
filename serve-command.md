## Serve Command

### Launch PHP Apps Without a Web Server

Why limit PHP to websites? The `phpkg serve` command lets you run any `phpkg`-compatible package as a standalone web app, straight from a Git URL or local path—no project install, no domain, no hassle. It spins up a local server using PHP’s built-in `php -S`, delivering your app’s entry point right to your browser.

- **Game-Changer**: Build and share web-ready tools or dashboards, no server setup needed.
- **Vision**: Expands PHP into a versatile app platform—think beyond the web.

*Requirements*: Needs the [PCNTL extension](https://www.php.net/manual/en/book.pcntl.php)—Unix/Linux/macOS only (no Windows yet).

---

### Usage

Pass a Git URL or local path to `phpkg serve`:

#### From a Git URL

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
  
#### Pick an Entry Point

Multiple entry points in `phpkg.config.json`? Choose one:  
```bash
phpkg serve https://github.com/php-repos/daily-routine.git dashboard.php
```

- **Default**: Serves the first entry point listed.  
- **Must-Have**: Package needs at least one entry point—see [Customization](https://phpkg.com/documentations/customization).

#### Set a Version

- Latest release by default. For a specific version:  

    ```bash
    phpkg serve https://github.com/php-repos/daily-routine.git --version=v1.0.0
    ```
- Dev version with a commit:  
    ```bash
    phpkg serve https://github.com/php-repos/daily-routine.git --version=development#f2ffcee641009d753c72a935a083b2fc650787c1
    ```

#### From a Local Path

Serve a package on your machine:  

```bash
phpkg serve ../relative/path/to/package
phpkg serve /absolute/path/to/package
```

- Ideal for dev testing.

_How It Works_: Downloads (or uses local), builds in a temp sandbox, and serves via `php -S` (e.g., `localhost:8000`). Cleanup happens on OS restart—no project changes.

---

### Why It Matters

PHP can do more than web pages—and `serve` proves it:

- **Instant Apps**: Launch dashboards or tools (e.g., `daily-routine`) without Apache or Nginx.  
- **No Overhead**: Skip project dependencies—run standalone, anywhere.  
- **Creative Freedom**: Build web-accessible PHP apps for yourself or others, no domain required.

Unlike Composer’s web-only focus, `phpkg serve` turns PHP into a universal app runner.

---

### Example

Serve the `daily-routine` package—a dashboard for your day:  

```bash
phpkg serve https://github.com/php-repos/daily-routine.git
```

- Output: Open `http://localhost:8000` to see tasks, crypto prices, news, and weather.
- No Setup: Just one command, no server config.

---

### Tips

- **Access**: Visit `localhost:8000` (or the port shown) in your browser.  
- **Tokens**: GitHub rate limits? Add a token via [Credential Command](https://phpkg.com/documentations/credential-command).  
- **Entry Points**: Check `phpkg.config.json` for options—see [Customization](https://phpkg.com/documentations/customization).  
- **Keep It**: Want it permanent? Use **phpkg add** instead.  
- **Pair It**: Use **phpkg run** for CLI output—see [Run Command](https://phpkg.com/documentations/run-command).
