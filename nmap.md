# nmap

## What it is
The go-to network scanner for port scanning, service/version detection, OS fingerprinting, and running NSE scripts. Foundation of any recon phase.

## Installation
```bash
sudo apt install nmap
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-sS` | SYN scan (stealth, requires root) |
| `-sV` | Service/version detection |
| `-sC` | Run default NSE scripts |
| `-O` | OS detection |
| `-p` | Port range (`-p 80,443` or `-p-` for all) |
| `-T<0-5>` | Timing (T4 = fast, T5 = aggressive) |
| `-oA` | Save output (all formats) |
| `-oN` | Save normal text output |
| `--script` | Run specific NSE script(s) |
| `-Pn` | Skip host discovery (treat as alive) |
| `-iL` | Input from file |
| `--open` | Show only open ports |

---

## Examples

**Quick scan (top 1000 ports)**
```bash
nmap example.com
```

**Full port scan with service detection**
```bash
nmap -sV -p- example.com
```
*Scans all 65535 ports, detects service versions.*

**Aggressive scan (version + scripts + OS)**
```bash
nmap -sV -sC -O example.com
```

**Fast scan with timing**
```bash
nmap -T4 --open example.com
```

**Scan specific ports**
```bash
nmap -p 22,80,443,8080 example.com
```

**Scan a subnet**
```bash
nmap -sn 192.168.1.0/24
```
*Ping sweep — discovers live hosts without port scanning.*

**Save results to file**
```bash
nmap -sV -sC -oA scan_results example.com
```
*Creates `.nmap`, `.xml`, `.gnmap` files.*

**Run HTTP vuln scripts**
```bash
nmap -p 80,443 --script http-vuln* example.com
```

**Scan from file, skip ping**
```bash
nmap -iL targets.txt -Pn -sV
```


## Important Setup & Advanced Tips
- **Nmap Scripting Engine (NSE)**: The real power of Nmap. Use `--script vuln` to check for common CVEs, or `--script http-enum` to enumerate directories.
- **Timing Templates**: Use `-T4` for faster scanning on reliable networks, but drop to `-T2` if you are getting dropped packets or encountering firewalls.
- **Output All Formats**: Always use `-oA <filename>` to save results in Grepable, XML, and Normal formats simultaneously.


## Professional Tips & Tricks
- **Min Rate**: To speed up Nmap significantly, use `--min-rate 1000`. Be careful, as this might crash fragile IoT devices.
- **Grepable Output**: Always use `-oA`. The `.gnmap` format allows you to easily `grep` for specific open ports across hundreds of hosts (e.g., `awk '/80\/open/ {print $2}' scan.gnmap`).
