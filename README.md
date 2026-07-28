# GitHub Recon

Prefer authenticated recon to access all operators.

| Operator      | Example                               |
| ------------- | ------------------------------------- |
| Specific file | `owner:megacorpone path:users`        |
| JS files      | `owner:megacorpone path:/src/**/*.js` |

**Automation tools:** `gitleaks`, `gitrob`

#### Github .git folder Recon&#x20;

```
# View the full commit history with diffs (find everything)
git log -p --all --full-history

# Display one-line log with graph (visualize branches)
git log --oneline --graph --all --decorate

# Show specific commit 
git show <commit-hash>

# Grep history for useful keywords
git log --all --grep="password\|secret\|key\|token\|api_key\|credential\|auth"
```
