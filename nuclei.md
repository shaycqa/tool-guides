# nuclei

## What it is
A fast, template-based vulnerability scanner by ProjectDiscovery. Uses YAML templates to detect CVEs, misconfigs, exposures, and more across thousands of hosts.

## Installation
```bash
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

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


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com
http://192.168.1.15:8080
```

**Output File (`results.txt`)**
```text
[cve-2021-44228] [http] [critical] https://example.com/?q=${jndi:ldap://...}
[tech-detect] [http] [info] http://192.168.1.15:8080 [Apache Tomcat]
```

## Important Nuclei Tags

Nuclei uses tags to group templates. You can filter which templates to run by passing `-t` (directory) or `-tags` (comma separated tags).

| Tag | Description |
| :--- | :--- |
| `cve` | Templates checking for publicly disclosed CVEs. |
| `misconfig` | Checks for missing headers, weak configurations, and setup errors. |
| `exposures` | Looks for exposed configs, `.env` files, backups, and git folders. |
| `auth-bypass` | Vulnerabilities that allow bypassing authentication mechanisms. |
| `sqli` | SQL Injection tests. |
| `xss` | Cross-Site Scripting (XSS) tests. |
| `ssrf` | Server-Side Request Forgery tests. |
| `lfi` | Local File Inclusion and path traversal vulnerabilities. |
| `rce` | Remote Code Execution tests (highly critical). |
| `fuzz` | Advanced fuzzing templates for hunting unknown vulnerabilities. |
| `tech` | Technology detection (e.g., identifying WordPress, React, Apache). |
| `osint` | OSINT-related templates, credential checks against APIs, etc. |
| `cloud` | Specific checks for AWS, Azure, GCP buckets and misconfigurations. |
| `token-spray` | Validates exposed API keys and tokens by attempting to authenticate. |
| `network` | Lower-level network and service checks (requires Nmap integration in some cases). |
| `iot` | Checks targeting default credentials and vulns in routers, cameras, and IoT devices. |

**Example:**
```bash
nuclei -u https://example.com -tags cve,rce,exposures
```

## Creating Custom Templates

Nuclei's true power lies in its YAML-based templating engine. Creating your own templates allows you to hunt for specific internal vulnerabilities, custom bypasses, or newly released zero-days before official templates are published.

### 1. Basic Template Structure
Every Nuclei template follows a standard structure consisting of an `id`, an `info` block, and the protocol-specific request (e.g., `http`, `dns`, `network`).

```yaml
id: my-custom-detection

info:
  name: Custom Vulnerability Detection
  author: your-name
  severity: high
  description: Brief description of what this template detects.
  tags: custom, auth-bypass

http:
  - method: GET
    path:
      - "{{BaseURL}}/admin/config.json"

    matchers:
      - type: word
        words:
          - "db_password"
          - "api_key"
        condition: or
        part: body

      - type: status
        status:
          - 200
```

### 2. Key Components Explained
*   **`id`**: A unique, lowercase string (no spaces) used to identify the template.
*   **`info`**: Metadata about the template (`severity` and `tags` are highly recommended).
*   **`path`**: Supports dynamic variables like `{{BaseURL}}` (the target URL provided via `-u`) or `{{Hostname}}`.
*   **`matchers`**: Logic to determine if the vulnerability exists.
    *   `type: word`: Looks for specific strings.
    *   `type: status`: Checks the HTTP response code.
    *   `type: regex`: Uses regular expressions for complex matching.
    *   `part`: Specifies where to look (`body`, `header`).
    *   `condition`: When using multiple words, specifies if `and` / `or` logic should be applied.

### 3. Testing Your Template
Before running your template at scale, validate its syntax and test it against a target:

**Validate Syntax:**
```bash
nuclei -validate -t my-custom-template.yaml
```

**Test Against a Target (with debug mode):**
```bash
nuclei -t my-custom-template.yaml -u https://example.com -debug
```
*The `-debug` flag is crucial when developing templates as it shows the exact raw HTTP request sent and the raw response received.*
