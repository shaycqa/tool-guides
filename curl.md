# curl

## What it is
A command-line tool for transferring data to/from servers using HTTP, HTTPS, FTP, and more. Essential for manual HTTP request crafting in recon and testing.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-X` | HTTP method (GET, POST, PUT, DELETE) |
| `-H` | Add custom header |
| `-d` | Send POST data |
| `-o / -O` | Save output to file |
| `-I` | Fetch headers only |
| `-L` | Follow redirects |
| `-u` | Basic auth (user:pass) |
| `-b` | Send cookie |
| `-k` | Skip SSL verification |
| `--proxy` | Route through proxy |

---

## Examples

**Fetch a page**
```bash
curl https://example.com
```
*Gets the raw HTML of the page.*

**View response headers only**
```bash
curl -I https://example.com
```
*Useful to check server, content-type, redirects.*

**POST JSON data**
```bash
curl -X POST -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"test"}' \
  https://example.com/api/login
```
*Sends a JSON login request.*

**Send with custom cookie and header**
```bash
curl -H "Authorization: Bearer TOKEN" \
  -b "session=abc123" \
  https://example.com/api/profile
```
*Useful for authenticated requests.*

**Follow redirects and save output**
```bash
curl -L -o response.html https://example.com
```

**Route through Burp Proxy**
```bash
curl -k --proxy http://127.0.0.1:8080 https://example.com
```
*`-k` skips SSL check, useful when Burp intercepts HTTPS.*

**Upload a file**
```bash
curl -F "file=@shell.php" https://example.com/upload
```

**Basic auth**
```bash
curl -u admin:password https://example.com/admin
```


## Important Setup & Advanced Tips
- **Path Traversal**: Use `--path-as-is` so curl doesn't squash `../` sequences before sending the request.
- **Timing & Performance**: Use `-w` (write-out) to measure response times: `curl -w "%{time_total}\n" -o /dev/null -s http://example.com`.
- **Proxying**: Easily send traffic through Burp Suite for inspection: `-x http://127.0.0.1:8080`.
