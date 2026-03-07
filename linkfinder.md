# linkfinder

## What it is
A Python script that extracts endpoints and parameters from JavaScript files. Finds hidden API paths, internal routes, hardcoded tokens, and forgotten dev endpoints — all from JS source code.

**Install:**
```bash
git clone https://github.com/GerbenJavado/LinkFinder.git
cd LinkFinder && pip3 install -r requirements.txt
```

## Installation
```bash
git clone https://github.com/GerbenJavado/LinkFinder.git
cd LinkFinder
pip install -r requirements.txt
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Input (JS file URL, local file, or JS bundle) |
| `-o` | Output format: `cli` (terminal) or `html` (report) |
| `-d` | Crawl a domain and find all JS files automatically |
| `-b` | Burp Suite XML file as input |
| `-r` | Regex to filter output |

---

## Examples

**Analyze a single JS file from URL**
```bash
python3 linkfinder.py -i https://example.com/static/app.js -o cli
```
*Extracts all endpoints found in that JS file.*

**Analyze a local JS file**
```bash
python3 linkfinder.py -i ./bundle.js -o cli
```

**Crawl a whole domain for JS endpoints**
```bash
python3 linkfinder.py -i https://example.com -d -o cli
```
*Finds all JS files on the site and extracts endpoints from all of them.*

**Generate an HTML report**
```bash
python3 linkfinder.py -i https://example.com -d -o results.html
```

**Filter for API paths only**
```bash
python3 linkfinder.py -i https://example.com/app.js -o cli | grep "/api/"
```

**Common workflow**
```bash
# 1. Crawl site with katana to collect JS URLs
katana -u https://example.com -jc -silent | grep "\.js$" > jsfiles.txt

# 2. Run linkfinder on each JS file
while read url; do
  python3 linkfinder.py -i "$url" -o cli
done < jsfiles.txt
```
*Extracts all hidden endpoints from every JavaScript file on the target.*


## Important Setup & Advanced Tips
- **Execution Pipeline**: Best used in an automated loop: download JS files with `subjs` -> feed to `LinkFinder` -> parse paths to `httpx`.
- **Input Flexibility**: Can parse local directories, single files, or remote URLs directly.
- **Burp Integration**: LinkFinder has a Burp Suite extension version which is highly recommended for manual testing.
