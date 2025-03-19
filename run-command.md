## Run Command

### Unleash PHP Tools Anywhere

Imagine running a PHP tool—like a static analyzer or a weather checker—without embedding it in a project or fussing with dependencies. The `phpkg run` command makes this real: it grabs any `phpkg`-compatible Git repository, builds it on the fly, and executes it right in your terminal. No installs, no web servers—just pure PHP power at your fingertips.

- **Why It’s Revolutionary**: Turns PHP into a tool-runner, not just a web engine.
- **Big Idea**: Stop bloating projects with dev tools—run them standalone, once per machine.

---

### Usage

Pass a Git URL or local path to `phpkg run`:

#### From a Git URL

```bash
phpkg run <package-url> [entry-point]
```

- **HTTPS**:  
    ```bash
    phpkg run https://github.com/owner/repo.git
    ```
- **SSH**:  

    ```bash
    phpkg run git@github.com:owner/repo.git
    ```

#### Pick an Entry Point

Multiple entry points in `phpkg.config.json`? Specify one:  

```bash
phpkg run https://github.com/php-repos/chuck-norris.git jokes.php
```

- Default: Runs the first entry point listed.

#### Set a Version

- Latest release by default. For a specific version:  

    ```bash
    phpkg run https://github.com/php-repos/weather.git --version=v1.2.3
    ```

- Dev version with a commit:  
    ```bash
    phpkg run https://github.com/php-repos/chuck-norris.git --version=development#336212f42b0d612a1397e5009f2e3c681851d770
    ```

#### From a Local Path

Test a package on your machine:  
```bash
phpkg run ../relative/path/to/package
phpkg run /absolute/path/to/package
```

**How It Works**: Downloads (or uses local), builds in a temp sandbox, runs the entry point, and cleans up on reboot—no project changes.

---

### Why It Matters

PHP isn’t just for websites—it’s for tools. The `run` command breaks the mold:

- **Standalone Power**: Run analyzers (e.g., PHPStan) or utilities without project bloat.  
    ```bash
    phpkg run https://github.com/phpstan/phpstan.git phpstan analyze /path/to/project
    ```
- **Real Apps**: Build CLI tools—like a daily dashboard—usable anywhere.  
    ```bash
    phpkg run https://github.com/php-repos/daily-routine.git
    ```
- **Efficiency**: Install once globally, not per project—less waste, faster setups.

Unlike Composer, which ties tools to `vendor/`, `phpkg run` frees them to stand alone, slashing redundancy and complexity.

### Examples

- Chuck Norris Jokes:

    ```bash
    phpkg run https://github.com/php-repos/chuck-norris.git
    ```

    Output: A Chuck Norris quip from https://api.chucknorris.io/.

- Weather Check:  

    ```bash
    phpkg run https://github.com/php-repos/weather.git
    ```
    Output: Your local forecast in the terminal.

- Static Analysis:  
    ```bash
    phpkg run https://github.com/phpstan/phpstan.git phpstan analyze ./my-app
    ```
    Output: Code analysis, no install needed.
---

### Tips

- **Tokens**: GitHub rate limits? Add a token via [Credential Command](https://phpkg.com/documentations/credential-command).  
- **Entry** Points: See a package’s `phpkg.config.json` for options—check [Customization](https://phpkg.com/documentations/customization).  
- **Keep It**: Want it permanent? Use `phpkg add` instead.  
- **Dream Big**: Create your own CLI tools—PHP’s limits are yours to break.

_Companion_: Pair with `phpkg serve` for web-ready apps—see [Serve Command](https://phpkg.com/documentations/serve-command).
