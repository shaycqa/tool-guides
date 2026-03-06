# jwt_tool

## What it is
A toolkit by ticarpi for testing, tweaking, and cracking JSON Web Tokens (JWTs). It automates common attacks like algorithm confusion, null signatures, and brute-forcing.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-t` | Target URL to send the modified token to |
| `-rh` | Request headers (e.g. 'Authorization: Bearer <jwt>') |
| `-M` | Mode of operation (pb = playbooks, at = all tests) |
| `-C` | Crack the token signature using a dictionary |
| `-d` | Dictionary file for cracking |

---

## Examples

**Run all automated tests against a token**
```bash
python3 jwt_tool.py <jwt_token> -M at
```

**Crack a JWT signature using a wordlist**
```bash
python3 jwt_tool.py <jwt_token> -C -d /usr/share/wordlists/rockyou.txt
```

**Modify token payload interactively**
```bash
python3 jwt_tool.py <jwt_token> -I
```

**Test token against an endpoint**
```bash
python3 jwt_tool.py <jwt_token> -t https://api.example.com/user -rh 'Authorization: Bearer ' -M pb
```


## Important Setup & Advanced Tips
- **Advanced Attacks**: Use `-X k` for Key Confusion (RS256 to HS256) and `-X I` for JWK/JKU Header Injection.
- **Tampering**: You can base64 encode/decode and manually sign tokens within the interactive mode (`-I`).
- **Public Keys**: If you find the server's public key, you can provide it to `jwt_tool` to forge HS256 tokens in a Key Confusion attack.
