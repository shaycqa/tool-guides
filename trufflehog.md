# trufflehog

## What it is
A tool that finds and verifies exposed secrets in source code, commit history, and various other sources like GitHub, GitLab, and filesystems.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `git` | Scan a git repository |
| `github` | Scan a GitHub organization or user |
| `filesystem` | Scan a local directory |
| `--only-verified` | Only output verified credentials |
| `--json` | Output results in JSON format |
| `--no-update` | Do not check for updates |

---

## Examples

**Scan a public git repository**
```bash
trufflehog git https://github.com/example/repo.git
```

**Scan a local directory**
```bash
trufflehog filesystem /path/to/code
```

**Scan an entire GitHub organization**
```bash
trufflehog github --org example-org
```

**Show only verified secrets (reduces noise)**
```bash
trufflehog git https://github.com/example/repo.git --only-verified
```

**Output results as JSON**
```bash
trufflehog filesystem ./src --json > secrets.json
```


## Important Setup & Advanced Tips
- **CI/CD Integration**: TruffleHog is frequently used in GitHub Actions or GitLab CI to prevent secrets from being committed in the first place.
- **Concurrency**: Use `--concurrency` to speed up scans on large repositories or entire organizations.
- **Custom Rules**: You can build and pass custom YAML rules to look for proprietary token formats.
