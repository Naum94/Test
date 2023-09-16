# Linux cheatsheet
### BASH Customizations

Colors
```bash
RED="\[\e[1;31m\]";
GREEN="\[\e[1;32m\]";
YELLOW="\[\e[1;33m\]";
BLUE="\[\e[1;34m\]";
PURPLE="\[\e[1;35m\]"; 
AQUA="\[\e[1;36m\]";
WHITE="\[\e[1;37m\]";
RESET="\[\e[0m\]";
```

BASH Prompt example
```bash
PS1="${GREEN}\u${WHITE}@${RED}\h ${WHITE}in ${AQUA}\w ${WHITE}> ${RESET}";
```

Aliases
```bash
alias grep='grep --color=auto'
alias nano='nano -ic'
```

### OPENSSL Tricks
Get all certificates for a given site
```bash
echo | openssl s_client -showcerts -connect www.example.com:443 | awk '/BEGIN CERT/,/END CERT/ {print $0}' > chain.pem
```

Get all certificates for a given site using SNI
```bash
echo | openssl s_client -showcerts -servername www.example.com -connect www.example.com:443 | awk '/BEGIN CERT/,/END CERT/ {print $0}' > chain.pem
```

Read SSL certificate
```bash
openssl x509 -noout -text -in certificate.cer
```
Extract certificate chain from PFX
```bash
openssl pkcs12 -in certificate.pfx -nokeys -out ca-bundle.pem -nodes
```

Extract private key from PFX
```bash
openssl pkcs12 -in certificate.pfx -nocerts -out ca-bundle.pem -nodes
```

Remove private key passphrase
```bash
openssl rsa -in private_w_pf.key -out private.key
```
### CURL Tricks

Test HTTPS with certificate chain file
```bash
curl -vI --cacert ca-bundle.pem "https://www.example.com"
```

Check certificate validity for given site
```bash
curl -kvI https://example.com 2>&1 | awk '/Server certificate/,/issuer/ { print }'
```

### SCREEN Tricks
Create new screen session
```bash
screen -S {screen name}
```

Join screen session
```bash
screen -x {screen name}
```

Detach from screen 
```bash
screen -d
```

Re-attach to screen 
```bash 
screen -r {screen name}
```

Keybord Shortcuts
        
  - Detach from screen: ```Ctrl + a + Ctrl + d```
  - Split vertically: ```Ctrl + a + |```
  - Split horizontally: ```Ctrl + a + S```
  - Change window: ```Ctrl + a + Tab```
  - Start new screen session in window: ```Ctrl + a + Ctrl + c```
  - Exit all screen windows: ```Ctrl + a + \```
