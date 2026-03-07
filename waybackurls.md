# waybackurls

## What it is
A tool by tomnomnom that accepts line-delimited domains on stdin, fetches known URLs from the Wayback Machine for `*.domain`, and outputs them on stdout.

## Installation
```bash
go install github.com/tomnomnom/waybackurls@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-dates` | Show the date of the fetch |
| `-no-subs` | Don't include subdomains of the target domain |
| `-get-versions` | Get URLs for all versions of a file |

---

## Examples

**Fetch URLs for a domain**
```bash
echo example.com | waybackurls
```

**Fetch URLs for a list of domains**
```bash
cat domains.txt | waybackurls
```

**Fetch URLs and show the crawl dates**
```bash
echo example.com | waybackurls -dates
```

**Fetch URLs without including subdomains**
```bash
echo example.com | waybackurls -no-subs
```

**Save results to a file**
```bash
echo example.com | waybackurls > urls.txt
```


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Output File (`urls.txt`)**
```text
http://example.com/robots.txt
https://example.com/api/v1/users?id=1
https://test.com/login.php
```


## Professional Tips & Tricks
- **JSON Output for Extraction**: Use `-json` to get detailed output including the HTTP status code the Wayback Machine observed. You can `jq` this to find endpoints that returned 200 OK.
