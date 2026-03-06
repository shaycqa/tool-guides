# cewl

## What it is
CeWL (Custom Word List generator) crawls a website and generates a custom wordlist from the words found on the page. Useful for targeted password attacks and fuzzing.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-d` | Crawl depth (default: 2) |
| `-m` | Minimum word length |
| `-w` | Save output to file |
| `-e` | Extract email addresses |
| `-n` | Don't output word list (use with `-e`) |
| `-c` | Count word frequency |
| `-v` | Verbose mode |
| `--with-numbers` | Include words with numbers |
| `--debug` | Show debug info |

---

## Examples

**Basic crawl — print wordlist to terminal**
```bash
cewl https://example.com
```

**Save wordlist to file**
```bash
cewl https://example.com -w wordlist.txt
```

**Set minimum word length to 7**
```bash
cewl https://example.com -m 7 -w wordlist.txt
```
*Filters out short, common words.*

**Increase crawl depth**
```bash
cewl https://example.com -d 3 -w wordlist.txt
```
*Goes deeper into the site for more words.*

**Extract emails only**
```bash
cewl https://example.com -n -e
```

**Count word frequency**
```bash
cewl https://example.com -c
```
*Useful to see which words appear most often.*

**Include numbers (alpha-numeric wordlist)**
```bash
cewl https://example.com --with-numbers -w wordlist.txt
```

**Full options example**
```bash
cewl -d 2 -m 5 --with-numbers -w custom_wordlist.txt https://example.com
```
*Depth 2, min 5 chars, includes numbers — a good balance for targeted attacks.*
