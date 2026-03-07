# amass

## What it is
A comprehensive in-depth DNS enumeration and network mapping tool by OWASP. It performs active and passive discovery to map an organization's external attack surface.

## Installation
```bash
go install -v github.com/owasp-amass/amass/v4/...@master
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `enum` | Perform DNS enumeration and network mapping |
| `intel` | Discover targets for enumerations |
| `-d` | Target domain name |
| `-passive` | Only use passive data sources (no DNS resolution) |
| `-active` | Enable active reconnaissance (zone transfers, certificate pulling) |
| `-src` | Print data sources for the discovered names |
| `-o` | Output file |

---

## Examples

**Basic passive enumeration**
```bash
amass enum -passive -d example.com
```

**Active enumeration with sources shown**
```bash
amass enum -active -src -d example.com
```

**Discover ASN and IP ranges for an organization**
```bash
amass intel -org "Example Corp"
```

**Find related domains using ASN**
```bash
amass intel -asn 12345
```

**Save output to a text file**
```bash
amass enum -d example.com -o amass_results.txt
```


## Important Setup & Advanced Tips
- **API Keys**: Amass's true power comes from APIs. Configure them in `~/.config/amass/config.ini` and run with `-config ~/.config/amass/config.ini`.
- **Continuous Monitoring**: Use `amass track -d example.com` to see what changed since the last enumeration.
- **Visualization**: Use `amass viz -d3` to generate network graphs.
