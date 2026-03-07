# asnmap

## What it is
A fast ASN (Autonomous System Number) mapping tool by ProjectDiscovery. It maps an organization name, domain, IP, or ASN to their corresponding network CIDR ranges, helping identify all IP space owned by a target.

## Installation
```bash
go install -v github.com/projectdiscovery/asnmap/cmd/asnmap@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-d` | Target domain |
| `-a` | Target ASN number (e.g., AS1234) |
| `-ip` | Target IP address |
| `-org` | Target organization name |
| `-silent` | Only display results |
| `-json` | Output in JSON format |
| `-o` | Output file |

---

## Examples

**Map a domain to its CIDR ranges**
```bash
echo "target.com" | asnmap -silent
```

**Map an organization to its IP ranges**
```bash
asnmap -org "Company Name" -silent
```

**Map an ASN to CIDR ranges**
```bash
asnmap -a AS13335 -silent
```

**Map an IP to its ASN and CIDR**
```bash
asnmap -ip 1.1.1.1 -silent
```

**Pipe from subfinder for full ASN mapping**
```bash
subfinder -d target.com -silent | dnsx -silent -resp-only | asnmap -silent
```

**JSON output for programmatic use**
```bash
echo "target.com" | asnmap -json -silent
```


## Important Setup & Advanced Tips
- **API Key**: asnmap works without an API key using public data, but you can configure a ProjectDiscovery API key for better results.
- **Piping**: Output CIDR ranges can be piped directly into `mapcidr` for IP expansion or `naabu` for port scanning.
- **Multiple inputs**: You can pass a file of domains/IPs/ASNs via stdin: `cat domains.txt | asnmap -silent`.


## Input & Output Examples

**Input**
```text
target.com
```

**Output**
```text
192.168.0.0/16
10.0.0.0/8
172.16.0.0/12
```

**JSON Output**
```json
{"input":"target.com","as_number":13335,"as_name":"CLOUDFLARENET","as_country":"US","as_range":["104.16.0.0/13","172.64.0.0/13"]}
```


## Professional Tips & Tricks
- **Full attack surface**: Combine with mapcidr and dnsx for complete infrastructure mapping: `echo "target.com" | asnmap -silent | mapcidr -silent | dnsx -ptr -resp-only -silent`.
- **Scope validation**: Use asnmap to verify if discovered IPs actually belong to the target organization before testing.
- **Multiple sources**: Pipe organization name variations to catch all ASNs: `echo -e "Company Inc\nCompany LLC" | asnmap -silent | sort -u`.
