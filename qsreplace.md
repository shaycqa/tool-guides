# qsreplace

## What it is
A tool by tomnomnom to replace all query string values in a list of URLs with a custom payload. Essential for mass-testing XSS, SQLi, or SSRF payloads.

## Installation
```bash
go install github.com/tomnomnom/qsreplace@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-a` | Append the payload instead of replacing the original value |

---

## Examples

**Replace all parameter values with an XSS payload**
```bash
cat urls.txt | qsreplace '"><script>alert(1)</script>'
```

**Replace all parameter values with a blind SSRF payload**
```bash
cat urls.txt | qsreplace 'http://burpcollaborator.net'
```

**Append a payload instead of replacing**
```bash
cat urls.txt | qsreplace -a ' OR 1=1--'
```

**Remove all parameter values (leave them empty)**
```bash
cat urls.txt | qsreplace ''
```


## Important Setup & Advanced Tips
- **Blind SSRF**: The most common use case is replacing all parameters with a Burp Collaborator / Interactsh payload: `cat urls.txt | qsreplace "http://your-interactsh.com"`.
- **Appends**: Using `-a` appends the payload instead of replacing, which is useful for testing SQLi (e.g., appending `'` or `"`).
- **Multiple Replacements**: You can run it multiple times or use a bash loop to test a small list of highly effective payloads.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com/page.php?id=1
https://example.com/search?q=test
```

**Output (e.g., running `qsreplace 'XSS'`)**
```text
https://example.com/page.php?id=XSS
https://example.com/search?q=XSS
```


## Professional Tips & Tricks
- **Blind SSRF Testing**: `cat urls_with_params.txt | qsreplace 'http://<your-interactsh-id>' | httpx`. Check your interactsh client for pings.
- **SQLi Error Based**: `cat urls.txt | qsreplace "'" | httpx -mr 'SQL syntax'`.
