# mapcidr

## What it is
A CIDR/subnet manipulation utility by ProjectDiscovery. It performs various operations on CIDR ranges and IP addresses — expanding CIDRs to individual IPs, aggregating IPs into CIDRs, splitting/merging ranges, and filtering.

## Installation
```bash
go install -v github.com/projectdiscovery/mapcidr/cmd/mapcidr@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-cidr` | Target CIDR range |
| `-l` | List of CIDRs from file |
| `-silent` | Only display results |
| `-o` | Output file |
| `-aggregate` | Aggregate IPs into smallest CIDR ranges |
| `-count` | Count number of IPs in CIDR |
| `-skip-base` | Skip base (network) address |
| `-skip-broadcast` | Skip broadcast address |
| `-slices` | Split CIDR into N equal parts |
| `-sbc` | Split by CIDR size (e.g., /24) |
| `-filter-ipv4` | Filter only IPv4 addresses |
| `-filter-ipv6` | Filter only IPv6 addresses |
| `-shuffle` | Randomize IP order |

---

## Examples

**Expand a CIDR to individual IPs**
```bash
echo "192.168.1.0/24" | mapcidr -silent
```

**Aggregate IPs back into CIDRs**
```bash
cat ips.txt | mapcidr -aggregate -silent
```

**Count IPs in a CIDR**
```bash
echo "10.0.0.0/16" | mapcidr -count -silent
```

**Split a large CIDR into /24 subnets**
```bash
echo "10.0.0.0/16" | mapcidr -sbc 24 -silent
```

**Split a CIDR into 4 equal parts**
```bash
echo "192.168.0.0/22" | mapcidr -slices 4 -silent
```

**Pipe from asnmap to expand ranges**
```bash
echo "target.com" | asnmap -silent | mapcidr -silent
```

**Shuffle IPs for distributed scanning**
```bash
echo "192.168.1.0/24" | mapcidr -silent -shuffle
```


## Important Setup & Advanced Tips
- **Large ranges**: Be careful expanding large CIDRs (e.g., /16 = 65,536 IPs, /8 = 16M IPs). Use `-count` first to check.
- **Piping**: Commonly used between asnmap (get CIDRs) and dnsx/naabu (resolve/scan the IPs).
- **Deduplication**: mapcidr with `-aggregate` is useful for deduplicating overlapping CIDR ranges.


## Input & Output Examples

**Input (CIDRs)**
```text
192.168.1.0/30
```

**Output (Expanded IPs)**
```text
192.168.1.0
192.168.1.1
192.168.1.2
192.168.1.3
```

**Aggregation Input (IPs)**
```text
192.168.1.0
192.168.1.1
192.168.1.2
192.168.1.3
```

**Aggregation Output**
```text
192.168.1.0/30
```


## Professional Tips & Tricks
- **Full recon chain**: `echo "target.com" | asnmap -silent | mapcidr -silent | dnsx -ptr -resp-only -silent` — maps domain to ASN to IPs to reverse DNS hostnames.
- **Scope checking**: Use `-aggregate` to normalize a list of IPs/CIDRs, then compare against the program's defined scope.
- **Distributed scanning**: Use `-slices` to split work across multiple machines or scan sessions.
