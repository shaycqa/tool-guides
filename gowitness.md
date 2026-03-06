# gowitness

## What it is
A website screenshot utility written in Golang by sensepost, that uses Chrome Headless to generate screenshots of web interfaces using a provided list of URLs.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `single` | Take a screenshot of a single URL |
| `file` | Take screenshots from a file of URLs |
| `--url` | Target URL |
| `--file` | File containing URLs |
| `--threads` | Number of concurrent threads |
| `--timeout` | Timeout for page load |

---

## Examples

**Screenshot a single URL**
```bash
gowitness single --url https://example.com
```

**Screenshot a list of URLs from a file**
```bash
gowitness file -f urls.txt --threads 10
```

**Start a web server to view the report**
```bash
gowitness report server
```

**Take screenshots with a specific timeout**
```bash
gowitness file -f urls.txt --timeout 15
```
