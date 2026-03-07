# dnsx

## What it is
A fast and multi-purpose DNS toolkit by ProjectDiscovery. It allows you to run multiple DNS queries of your choice with a list of user-supplied resolvers.

## Installation
```bash
go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-l` | List of domains to resolve |
| `-d` | Target domain |
| `-a` | Query A record (default) |
| `-cname` | Query CNAME record |
| `-ptr` | Query PTR record |
| `-resp-only` | Display only the resolution results |
| `-silent` | Only display results |
| `-o` | Output file |

---

## Examples

**Resolve a list of domains**
```bash
dnsx -l domains.txt
```

**Only output the IPs (response only)**
```bash
dnsx -l domains.txt -resp-only
```

**Check for CNAME records**
```bash
dnsx -l domains.txt -cname
```

**Reverse DNS lookup (PTR) on CIDR**
```bash
echo 192.168.1.0/24 | dnsx -ptr -resp-only
```

**Pipe from subfinder to resolve subdomains**
```bash
subfinder -d example.com -silent | dnsx -silent
```


## Important Setup & Advanced Tips
- **Brute-Forcing**: dnsx can be used for subdomain bruteforcing with a wordlist: `dnsx -d example.com -w wordlist.txt`.
- **Custom Resolvers**: Always use a reliable list of resolvers to prevent rate-limiting/blocks: `dnsx -l domains.txt -r resolvers.txt`.
- **Wildcard Filtering**: Automatically filter out wildcard DNS records by adding `-wd`.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
api.example.com
dev.example.com
```

**Output File (`resolved.txt`)**
```text
api.example.com [192.168.1.15]
dev.example.com [10.0.0.5]
```


## Professional Tips & Tricks
- **Piping from other tools**: `subfinder -silent -d target.com | dnsx -silent -a -resp-only` is the fastest way to get a clean list of live IP addresses.
- **Wildcard Filtering**: Many domains have wildcard DNS. dnsx handles this gracefully, but if you want to explicitly check for it, you can use the `-wd` flag to output only valid records.
