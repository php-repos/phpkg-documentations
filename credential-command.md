## Credential Command

### Keep phpkg Running Smoothly with GitHub

Fetching lots of packages or ones with many releases? `phpkg` relies on GitHub’s API, and without a token, you might hit rate limits—even for public repos. The `credential` command adds your GitHub access token to unlock private repos *and* keep public requests flowing, all with one quick step.

*Skip this if your `GITHUB_TOKEN` env var is already set.*

---

### Usage
1. **Get a Token**: Grab one from [GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
    - Pick “repo” scope for private access; “public_repo” works for rate limits on public repos.
2. **Add It**: Run:
   ```bash
   phpkg credential github.com <your-token>
   ```

- Stores the token securely for phpkg to use with GitHub’s API.

**Works with GitHub now—GitLab and more coming soon.**

---

### Why It Matters

- **Rate Limits**: GitHub caps unauthenticated API calls—busy projects (e.g., many packages or releases) can hit this fast.  
- **Private Repos**: Access locked-down code without hassle.  
- **Smooth Workflow**: One token, no interruptions.

Test it with:

```bash
phpkg add https://github.com/sebastianbergmann/phpunit.git
```

No rate limit errors? You’re set! See [Add Command](https://phpkg.com/documentations/add-command) for more.
