# paramspider

## What it is
A tool by devanshbatham for mining parameters from web archives (Wayback Machine). Essential for discovering hidden parameters vulnerable to XSS, SQLi, or SSRF.

## Installation
```bash
git clone https://github.com/devanshbatham/paramspider
cd paramspider
pip install .
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-d` | Target domain |
| `-s` | Subdomain inclusion (set to false to exclude) |
| `-l` | List of domains to scan |
| `-e` | Extensions to exclude (e.g. woff,css,png) |
| `-o` | Output file |

---

## Examples

**Basic parameter mining for a domain**
```bash
paramspider -d example.com
```

**Mine parameters and exclude useless extensions**
```bash
paramspider -d example.com --exclude woff,css,js,png,svg,jpg
```

**Scan a list of domains**
```bash
paramspider -l domains.txt
```

**Save output to a specific file**
```bash
paramspider -d example.com -o params.txt
```


## Important Setup & Advanced Tips
- **Stream Mode**: In v2, use the `-s` flag to stream results directly to stdout, which is perfect for piping into `httpx` or `kxss`.
- **Rate Limiting**: Since it relies on the Wayback Machine API, it can sometimes time out on massive targets.
- **Hidden Params**: ParamSpider only finds *historically known* parameters. Use `Arjun` alongside it to brute-force unknown hidden parameters.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Output File (`params.txt`)**
```text
https://example.com/page.php?id=FUZZ
https://test.com/search?q=FUZZ
```


## Professional Tips & Tricks
- **Hidden Parameters**: Often, developers leave old API versions active. ParamSpider finds parameters from months or years ago that are still supported by the backend but removed from the frontend UI.
