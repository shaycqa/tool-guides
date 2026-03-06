# shodan

## What it is
The command-line interface for Shodan, the search engine for Internet-connected devices. Useful for discovering exposed infrastructure and ports.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `search` | Search the Shodan database |
| `host` | View all available information for an IP address |
| `info` | Display information about your API plan |
| `download` | Download search results and save them in a file |
| `parse` | Extract information from a downloaded file |
| `--fields` | Specify the fields to display in output |

---

## Examples

**Check information for a specific IP**
```bash
shodan host 8.8.8.8
```

**Search for a specific hostname**
```bash
shodan search "hostname:example.com" --fields ip_str,port,product
```

**Search by SSL certificate subject**
```bash
shodan search "ssl.cert.subject.CN:example.com"
```

**Search by organization name**
```bash
shodan search "org:\"Example Corp\""
```

**Download search results for offline analysis**
```bash
shodan download results_file "hostname:example.com"
```


## Important Setup & Advanced Tips
- **Initialization**: You must initialize the CLI with your API key first: `shodan init <API_KEY>`.
- **Monitoring**: Set up network alerts for your infrastructure: `shodan alert create "My Network" 198.51.100.0/24`.
- **Facets**: Get aggregate statistics using facets: `shodan search --facets port "org:Example"`.
