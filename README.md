# Secure Code Review
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

Misc:
- Check for files that list all application routes to discover hidden paths e.g. used for admin access
- Base 64 encoded sensitive data
- Registration forms sent in GET
- User input and how its added to DB
- Check if any functions are missing input validation
- Take regex from app and add to a local app to see how regex works and if it can be bypassed, much faster than against remote app if auth is used etc. 
- Check if any blacklists are used as opposed to whitelists, could be abused by different file extensions e.g. if extension `php` is blocked, `php5` or `PHP` might bypass.

Use either tools to search codebase for keywords:
- Sublime Text `Ctrl+Shift+F` for global search of keywords
- Grep
```
secret
password
token
encode
decode
filter
sanitize
sanitise
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

Weak Hashing Algs
```
SHA1
MD5
MD4
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
AKIA[0-9A-Z]{16} #AWS API keys 
```

## SAST
SAST (Static Application Security Testing)

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

Determine technologies used by codebase and then search for security rule sets https://semgrep.dev/r?cat=security to include as configs. e.g. https://semgrep.dev/p/clientside-js 

[Wappalyzer browser extension](https://www.wappalyzer.com/apps) can be used to assist with detecting client side technologies. Although it should be easy to check file extensions and modules/libraries used in the code.

To create rules https://r2c.dev/blog/2020/writing-semgrep-rules-a-methodology/ 

### Truffle Hog
Use [Truffle Hog](https://github.com/trufflesecurity/trufflehog) to search for secrets

**TO BE UPDATED**

### Attack Surface Detector
[Attack Surface Detector](https://owasp.org/www-project-attack-surface-detector/) reveiws source code and detects the endpoints of a web application, the parameters these endpoints accept, and the data type of those parameters.
- [Burp](https://portswigger.net/bappstore/47027b96525d4353aea5844781894fb1) addon can be installed from inside app.
- ZAP addon can be installed from inside app.

### SonarQube
[SonarQube](https://www.sonarqube.org/) can locally deploy as open source 
