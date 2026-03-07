# unfurl

## What it is
A Go-based CLI tool by tomnomnom used to extract specific parts of URLs provided via stdin. Extremely useful for isolating domains, paths, or query parameters.

## Installation
```bash
go install github.com/tomnomnom/unfurl@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Only output unique values |
| `-v` | Verbose mode (outputs URL parsing errors) |
| `domains` | Extracts the hostname |
| `paths` | Extracts the URL paths |
| `keys` | Extracts keys from the query string |
| `values` | Extracts values from the query string |
| `format` | Uses a custom format string to extract specific bits |

---

## Examples

**Extract unique domains**
```bash
cat urls.txt | unfurl -u domains
```

**Extract query parameter values**
```bash
echo 'https://example.com?id=123&name=sam' | unfurl values
```

**Extract query parameter keys**
```bash
cat urls.txt | unfurl keys | sort -u
```

**Custom format (Domain + Path)**
```bash
echo 'https://sub.example.com/api/v1' | unfurl format %d%p
```


## Important Setup & Advanced Tips
- **JSON Output**: Use `--json` to output parsed URL components as JSON for easy parsing with `jq`.
- **Extracting Endpoints**: You can extract the base path (without query strings) using `format` to find unique API endpoints.
- **Chaining**: Perfect for feeding into `ffuf` or `sqlmap`. E.g., `cat urls.txt | unfurl keys | sort -u > parameters.txt`.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com/api/v1/users?id=1&role=admin
https://test.com/login.php?redirect=/dashboard
```

**Output (e.g., using `keys` mode)**
```text
id
role
redirect
```


## Professional Tips & Tricks
- **Dynamic Wordlists**: Create a custom wordlist based on the target's actual naming conventions by extracting all paths and parameters: `cat urls.txt | unfurl paths | sort -u > custom_wordlist.txt`.
