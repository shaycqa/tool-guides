# arjun

## What it is
A hidden HTTP parameter discovery tool. Fuzzes GET/POST/JSON parameters to find undocumented or hidden inputs in web applications. Has a built-in dictionary of 10,000+ parameter names.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Target URL |
| `-m` | HTTP method (`GET`, `POST`, `JSON`, `XML`) |
| `-o` | Save output to file (JSON) |
| `-oT` | Save output as plain text |
| `-w` | Custom wordlist |
| `-t` | Threads |
| `--stable` | Slower but more accurate |
| `--include` | Always include specific params |
| `--passive` | Use passive sources only |
| `-q` | Quiet mode |

---

## Examples

**Discover GET parameters**
```bash
arjun -u https://example.com/search
```

**Discover POST parameters**
```bash
arjun -u https://example.com/login -m POST
```

**Discover JSON body parameters**
```bash
arjun -u https://example.com/api/user -m JSON
```

**Use a custom wordlist**
```bash
arjun -u https://example.com/product -w params.txt
```

**Save results to file**
```bash
arjun -u https://example.com/api -o results.json
```

**Stable mode (more accurate, slower)**
```bash
arjun -u https://example.com/search --stable
```

**Force include specific params**
```bash
arjun -u https://example.com/page --include "id,user"
```
*Useful when you already suspect certain parameter names.*

**Common follow-up workflow**
```bash
# 1. Find hidden params
arjun -u https://example.com/api/search -m GET -o params.json

# 2. Use discovered params for fuzzing with ffuf
ffuf -u "https://example.com/api/search?id=FUZZ" -w ids.txt
```
