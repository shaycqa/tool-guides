# gf

## What it is
A wrapper around grep by tomnomnom, to help you quickly search for common vulnerability patterns (SQLi, XSS, SSRF, LFI) in large lists of URLs or files.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-list` | List all available patterns |
| `-dump` | Print the grep command instead of executing it |

---

## Examples

**List all available vulnerability patterns**
```bash
gf -list
```

**Find potential XSS parameters in a list of URLs**
```bash
cat urls.txt | gf xss
```

**Find potential SQLi parameters**
```bash
cat urls.txt | gf sqli
```

**Find interesting file extensions**
```bash
cat urls.txt | gf interestingEXT
```

**Find potential SSRF targets**
```bash
cat urls.txt | gf ssrf
```


## Important Setup & Advanced Tips
- **Installing Patterns**: `gf` is empty by default. You MUST clone a pattern repository (like `1ndianl33t/Gf-Patterns`) and copy the `.json` files to `~/.gf/`.
- **Custom Patterns**: You can easily create your own JSON pattern files to grep for company-specific internal domains or specific framework errors.
- **Dump Flag**: Use `-dump` to see the actual raw grep command `gf` is running behind the scenes.
