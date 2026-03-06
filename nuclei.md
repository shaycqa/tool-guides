# nuclei

## What it is
A fast, template-based vulnerability scanner by ProjectDiscovery. Uses YAML templates to detect CVEs, misconfigs, exposures, and more across thousands of hosts.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Single target URL |
| `-l` | File with list of targets |
| `-t` | Specify template or folder |
| `-tags` | Filter templates by tag (e.g., cve, xss) |
| `-severity` | Filter by severity (low, medium, high, critical) |
| `-rl` | Rate limit (requests per second) |
| `-o` | Output file |
| `-json` | Output in JSON format |
| `-silent` | Only print results |
| `-update-templates` | Update community templates |

---

## Examples

**Scan a single target (all default templates)**
```bash
nuclei -u https://example.com
```
*Runs thousands of templates against the target automatically.*

**Scan a list of hosts**
```bash
nuclei -l hosts.txt
```

**Run only CVE templates**
```bash
nuclei -u https://example.com -tags cve
```

**Run only high/critical severity**
```bash
nuclei -u https://example.com -severity high,critical
```

**Pipe from subfinder + httpx**
```bash
subfinder -d example.com -silent | httpx -silent | nuclei -t technologies/
```
*Full recon-to-scan pipeline.*

**Save results to file**
```bash
nuclei -l targets.txt -o results.txt -json
```

**Scan with a specific template**
```bash
nuclei -u https://example.com -t cves/2021/CVE-2021-44228.yaml
```
*Target a specific known vulnerability (e.g., Log4Shell).*

**Update templates**
```bash
nuclei -update-templates
```


## Important Setup & Advanced Tips
- **Template Updates**: Always run `nuclei -ut` before scanning to ensure you have the latest vulnerability templates.
- **Rate Limiting**: To avoid WAF bans, use `-rl` (rate limit) and `-c` (concurrency) flags carefully.
- **Workflow Usage**: Use `-w` to run predefined workflows (e.g., `workflows/wordpress-workflow.yaml`) rather than blindly firing all templates.
