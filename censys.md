# censys

## What it is
Command-line interface for the Censys search engine, designed to discover internet-facing devices and services using active scanning data.

## Installation
```bash
pip install censys
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `search` | Search the Censys index |
| `--index-type` | Index to query (certs, hosts) |
| `--pages` | Number of pages of results to fetch |
| `--output` | Output format (json, screen) |

---

## Examples

**Search for hosts matching a domain**
```bash
censys search "services.tls.certificates.leaf.names: example.com"
```

**Search for specific software**
```bash
censys search "services.software.vendor: Apache"
```

**Search certificates by common name**
```bash
censys search --index-type certs "parsed.subject.common_name: example.com"
```

**Output search results to JSON**
```bash
censys search "example.com" --output json > results.json
```


## Important Setup & Advanced Tips
- **Configuration**: Run `censys config` to set up your API ID and Secret.
- **ASM (Attack Surface Management)**: The CLI also supports interacting with Censys ASM via the `censys asm` subcommand.
- **Dorking**: You can use complex boolean logic and regular expressions in your search queries.
