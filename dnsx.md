# dnsx

## What it is
A fast and multi-purpose DNS toolkit by ProjectDiscovery. It allows you to run multiple DNS queries of your choice with a list of user-supplied resolvers.

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
