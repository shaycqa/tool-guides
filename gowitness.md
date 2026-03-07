# gowitness

## What it is
A website screenshot utility written in Golang by sensepost, that uses Chrome Headless to generate screenshots of web interfaces using a provided list of URLs.

## Installation
```bash
go install github.com/sensepost/gowitness@latest
```

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


## Important Setup & Advanced Tips
- **Authentication**: You can pass headers for authenticated screenshots: `--header "Authorization: Bearer token"`.
- **Delay**: SPAs (Single Page Applications) often take time to render. Use `--delay 3` to wait 3 seconds before taking the screenshot.
- **Visual Recon**: Use the `gowitness report server` command to quickly scroll through hundreds of subdomains and visually identify interesting admin panels or default installations.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com
https://test.com
```

**Output**
```text
Directory with screenshot images (e.g., `https-example.com.png`, `https-test.com.png`)
```
