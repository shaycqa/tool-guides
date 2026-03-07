# ripgrep (rg)

## What it is
An extremely fast search tool that recursively searches files for regex or literal patterns. Like `grep` but much faster and smarter — respects `.gitignore`, supports Unicode, and highlights matches.

## Installation
```bash
sudo apt install ripgrep
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Case-insensitive search |
| `-n` | Show line numbers (default: on) |
| `-l` | Only show filenames with matches |
| `-c` | Count matches per file |
| `-r` | Replacement string (don't modify files, just display) |
| `--type / -t` | Filter by file type (e.g., `py`, `js`, `html`) |
| `-g` | Glob pattern for file filtering |
| `-e` | Specify pattern (useful with multiple patterns) |
| `-A / -B / -C` | Lines after/before/around match |
| `--no-ignore` | Don't respect `.gitignore` |
| `--hidden` | Search hidden files |
| `-o` | Only print matching part of line |

---

## Examples

**Search for a word in a file**
```bash
rg "password" config.py
```

**Search recursively in a directory**
```bash
rg "api_key" ./src
```
*Searches all files in `./src` for `api_key`.*

**Case-insensitive search**
```bash
rg -i "token" .
```

**Search only Python files**
```bash
rg "import" -t py
```

**Use glob to target specific files**
```bash
rg "TODO" -g "*.js"
```

**Show 2 lines of context around match**
```bash
rg "error" logs.txt -C 2
```

**Only show filenames**
```bash
rg -l "secret" .
```

**Search hidden files and ignore .gitignore rules**
```bash
rg "password" --hidden --no-ignore
```

**Regex search**
```bash
rg 'api[_-]?key\s*=' .
```
*Finds variations like `api_key=`, `apikey =`, `api-key=`.*

**Count occurrences per file**
```bash
rg -c "error" ./logs
```


## Important Setup & Advanced Tips
- **Context**: Use `-C 3` to show 3 lines of context around the match, or `-A` (after) / `-B` (before).
- **File Types**: Search only in specific file types easily: `rg -t js "API_KEY"`.
- **Regex Support**: By default, `rg` supports standard regex. Use `-e` to explicitly define regex, or `-F` for fixed string matching (much faster).
