## ----
[Home](index.md)
# Code Review
## Sites to Review
Review sites and add any useful info to the below:
- https://vickieli.dev/hacking/code-review-101/
- https://www.hackedu.com/blog/secure-code-review-best-practices
- https://docs.guardrails.io/docs/category/vulnerabilities
- https://github.com/softwaresecured/secure-code-review-checklist

## Manual Checks
Identify where user input is received and handled:
- Sources
- Sinks
- Any transormations that occur on the data that flows from source to sink

Check for any configure files as they contain config relating to:
- Authentication
- Authorisation
- File Upload
- DB Access

- Check for files that list all application routes to discover hidden paths e.g. used for admin access
- Base 64 encoded sensitive data
- Registration forms sent in GET
- User input and how its added to DB
- Check if any functions are missing input validation
- Take regex from app and add to a local app to see how regex works and if it can be bypassed, much faster than against remote app if auth is used etc. 

Use either tools to search codebase for keywords (will be covered in SAST too):
- Sublime Text Ctrl+Shift+F for global search of keywords
- Grep
```
secret
password
token
encode
decode
filter
sanitize
log
http
```

Check for tools used:
```
curl
wget
```

Check for SQL statements:
```
SELECT
INSERT
DELETE
UPDATE
```

Hashing Algs
```
SHA1
MD5
```

Any functions that exeute code
```
eval(
exec
execute
os.
```

Sublime supports regex searching, you need to enable regex on left of search popup `.*`
```
AWS API keys `AKIA[0-9A-Z]{16}`
```

## SAST
SAST (Static application security testing)

### Semgrep CLI 
Install:
```bash
python3 -m pip install semgrep
```

Add semgrep to PATH for easier use of the tool, default install for me on kali was `~/.local/bin/semgrep`

Example use:
```bash
semgrep --config "p/security-audit" --config "p/owasp-top-ten" --config "p/javascript" --metrics off -v -o output_file local_repo_folder_name
```

Search for rules https://semgrep.dev/r  e.g. https://semgrep.dev/p/security-audit for security audit above

To create rules https://r2c.dev/blog/2020/writing-semgrep-rules-a-methodology/ 

### Truffle Hog
Use [Truffle Hog](https://github.com/trufflesecurity/trufflehog) to search for secrets

**TO BE UPDATED**

### Attack Surface Detector
Burp or ZAP addons

### SonarQube
Can locally deploy as open source

## DAST
DAST (Dynamic application security testing)
