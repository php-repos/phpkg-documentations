# Credential Command

## Keep phpkg Running Smoothly with GitHub

Fetching lots of packages or ones with many releases? `phpkg` relies on GitHub's API, and without a token, you might hit rate limits—even for public repos. The `credential` command adds your GitHub access token to unlock private repos *and* keep public requests flowing, all with one quick step.

*Skip this if your `GITHUB_TOKEN` env var is already set.*

---

## Usage
1. **Get a Token**: Grab one from [GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
    - Pick "repo" scope for private access; "public_repo" works for rate limits on public repos.
2. **Add It**: Run:
   ```bash
   phpkg credential github.com <your-token>
   ```

- Stores the token securely for phpkg to use with GitHub's API.

**Works with GitHub now—GitLab and more coming soon.**

---

## Why It Matters

- **Rate Limits**: GitHub caps unauthenticated API calls—busy projects (e.g., many packages or releases) can hit this fast.  
- **Private Repos**: Access locked-down code without hassle.  
- **Smooth Workflow**: One token, no interruptions.

## Examples

### Adding Credentials
```bash
# Add GitHub token
phpkg credential github.com ghp_your_token_here

# Test it works
phpkg add php-repos/observer
```

### Using Environment Variable (Alternative)
```bash
# Set environment variable (Unix/macOS)
export GITHUB_TOKEN=ghp_your_token_here

# Set environment variable (Windows PowerShell)
$env:GITHUB_TOKEN="ghp_your_token_here"

# phpkg will use this automatically
phpkg add php-repos/observer
```

## Token Permissions

When creating a GitHub token, ensure it has:
- **`repo` scope**: For private repositories
- **`public_repo` scope**: For public repositories (rate limit increase)

## Security Best Practices

- ✅ **Don't commit tokens**: Never commit `credentials.json` to version control
- ✅ **Use environment variables**: In CI/CD, use secrets/environment variables
- ✅ **Rotate tokens**: Regularly rotate your tokens
- ✅ **Minimal permissions**: Only grant necessary scopes

## Troubleshooting

**Token not working?**
1. Verify token is valid: `curl -H "Authorization: token YOUR_TOKEN" https://api.github.com/user`
2. Check token has correct scopes
3. Ensure token hasn't expired

**Still hitting rate limits?**
- Verify token is being used: Check with `phpkg -vv add package`
- Ensure `GITHUB_TOKEN` env var isn't overriding stored credentials

## Related Commands

- **[Add Command](https://phpkg.com/documentations/add-command)** - Add packages that may need credentials
- **[Update Command](https://phpkg.com/documentations/update-command)** - Update packages that may need credentials
- **[Install Command](https://phpkg.com/documentations/install-command)** - Install packages that may need credentials
- **[Run Command](https://phpkg.com/documentations/run-command)** - Run packages that may need credentials
- **[Serve Command](https://phpkg.com/documentations/serve-command)** - Serve packages that may need credentials
- **[Command Comparison](https://phpkg.com/documentations/command-comparison)** - When to use which command

## What's Next?

- **[Getting Started](https://phpkg.com/documentations/getting-started)** - Learn the basics of phpkg
- **[Troubleshooting](https://phpkg.com/documentations/troubleshooting)** - Solve authentication issues
- **[Best Practices](https://phpkg.com/documentations/best-practices)** - Security recommendations
- **[FAQ](https://phpkg.com/documentations/faq)** - Frequently asked questions
