# puredns

## What it is
A high-speed DNS resolver and subdomain bruteforcer. Uses `massdns` under the hood to resolve massive wordlists fast while accurately filtering out wildcard DNS entries and poisoned responses.

**Requires:** `massdns` installed and a resolvers list (e.g., from [trickest/resolvers](https://github.com/trickest/resolvers)).

## Installation
```bash
go install -v github.com/d3mondev/puredns/v2/cmd/puredns@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `bruteforce` | Subdomain bruteforce mode |
| `resolve` | Resolve a list of domains |
| `-r` | Path to resolvers file |
| `--resolvers-trusted` | Trusted resolvers for validation |
| `-w` | Wordlist (for bruteforce mode) |
| `-l` | Input list of domains (for resolve mode) |
| `--wildcard-tests` | Number of wildcard tests (default: 5) |
| `--write` | Save valid domains to file |
| `--write-wildcards` | Save wildcard roots to file |
| `-t` | Threads |

---

## Examples

**Bruteforce subdomains with a wordlist**
```bash
puredns bruteforce wordlist.txt example.com -r resolvers.txt
```
*Core use case — resolves every combination fast.*

**Save valid subdomains to file**
```bash
puredns bruteforce wordlist.txt example.com -r resolvers.txt --write valid.txt
```

**Resolve an existing list of domains**
```bash
puredns resolve domains.txt -r resolvers.txt
```
*Useful to validate subdomains from other tools.*

**Use trusted resolvers for wildcard validation**
```bash
puredns bruteforce wordlist.txt example.com \
  -r resolvers.txt \
  --resolvers-trusted trusted.txt \
  --write results.txt
```
*Reduces false positives from DNS poisoning.*

**Pipe from another tool**
```bash
cat potential_subs.txt | puredns resolve -r resolvers.txt
```

**Common workflow**
```bash
# 1. Generate candidates with subfinder + bruteforce wordlist
subfinder -d example.com -silent > subs.txt
cat subs.txt wordlist.txt | puredns resolve -r resolvers.txt --write valid_subs.txt
```


## Important Setup & Advanced Tips
- **Valid Resolvers**: Puredns requires a high-quality list of public resolvers to function correctly. Download lists from trickest/resolvers.
- **Wildcard Filtering**: It uses advanced machine learning/statistical models to bypass complex wildcard DNS setups, saving huge amounts of time.
- **Rate Limiting**: Use `-l` or `--rate-limit` to restrict queries per second so you don't overwhelm your own router or the resolvers.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Input File (`resolvers.txt`)**
```text
8.8.8.8
1.1.1.1
9.9.9.9
```

**Output File (`resolved_subdomains.txt`)**
```text
api.example.com
dev.example.com
admin.test.com
```


## Professional Tips & Tricks
- **Massive Wordlists**: PureDNS is fast enough to handle wordlists with billions of lines. Always resolve against a massive wordlist (like Assetnote's `best-dns-wordlist.txt`) and provide a clean list of public resolvers.
