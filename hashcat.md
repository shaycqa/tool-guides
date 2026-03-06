# hashcat

## What it is
The world's fastest password cracker. It supports highly optimized attacks on hundreds of different hashing algorithms.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-m` | Hash type (e.g., 0 for MD5, 16500 for JWT) |
| `-a` | Attack mode (0 = straight/dictionary, 3 = brute-force) |
| `-o` | Output file for cracked passwords |
| `--force` | Ignore warnings |
| `--show` | Show cracked passwords only |

---

## Examples

**Dictionary attack on MD5 hashes using rockyou.txt**
```bash
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

**Dictionary attack on JWT tokens (HS256)**
```bash
hashcat -m 16500 -a 0 jwt_tokens.txt /usr/share/wordlists/rockyou.txt
```

**Show already cracked passwords**
```bash
hashcat -m 0 hashes.txt --show
```

**Brute-force attack (e.g., 4-digit PINs)**
```bash
hashcat -m 0 -a 3 hashes.txt ?d?d?d?d
```


## Important Setup & Advanced Tips
- **Mask Attacks**: Use masks for known patterns (e.g., `?u?l?l?l?d?d?d?d` for a capital letter, 3 lowercase, 4 digits).
- **Rules**: Use rule files to mutate your wordlists automatically: `-r /usr/share/hashcat/rules/best64.rule`.
- **Hardware Optimization**: Use `-w 3` or `-w 4` to increase the workload profile for faster cracking on dedicated GPUs.


## Input & Output Examples

**Input File (`hashes.txt`)**
```text
5d41402abc4b2a76b9719d911017c592
7d793037a0760186574b0282f2f435e7
```

**Input File (`wordlist.txt`)**
```text
password123
admin
hello
hello123
```

**Output (CLI / `--show`)**
```text
5d41402abc4b2a76b9719d911017c592:hello
```
