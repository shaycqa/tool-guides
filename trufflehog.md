# trufflehog

## What it is
A tool that finds and verifies exposed secrets in source code, commit history, and various other sources like GitHub, GitLab, and filesystems.

## Installation
```bash
curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sh -s -- -b /usr/local/bin
```

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


## Professional Tips & Tricks
- **GitHub Actions**: Run TruffleHog against pull requests. In Bug Bounty, use it to scan the commit history of a public repository (`--since-commit`). Often, a developer commits a secret and then 'removes' it in the next commit. TruffleHog finds it.
- **Verified Only**: Always use `--only-verified`. It dramatically reduces false positives by actually attempting to authenticate with the discovered keys against the provider (e.g., AWS, GCP, Slack).
