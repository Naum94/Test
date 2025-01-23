# Linux cheatsheet

Aliases
```bash
alias grep='grep --color=auto'
alias nano='nano -ic'
```

### OPENSSL Tricks
Get all certificates for a given site
```bash
echo | openssl s_client -showcerts -connect www.example.com:443 \
| awk '/BEGIN CERT/,/END CERT/ {print $0}' > chain.pem
```

Get all certificates for a given site using SNI
```bash
echo | openssl s_client -showcerts -servername www.example.com -connect www.example.com:443 \
| awk '/BEGIN CERT/,/END CERT/ {print $0}' > chain.pem
```

Read CSR
```bash
openssl req -noout -text -in certificate.csr
```

Read SSL certificate
```bash
openssl x509 -noout -text -in certificate.cer
```

Extract certificate chain from PFX
```bash
openssl pkcs12 -in certificate.pfx -nodes -nokeys -out ca-bundle.pem
```

Extract private key from PFX
```bash
openssl pkcs12 -in certificate.pfx -nodes -nocerts -out ca-bundle.key
```

Remove private key passphrase
```bash
openssl rsa -in private_w_pf.key -out private.key
```

Create CSR with SAN's
```bash
openssl req -new -sha256 -nodes \
-newkey rsa:2048 -keyout example.key \
-subj "/C=MK/L=example/OU=IT/O=example/CN=www.example.com" \
-addext "subjectAltName=DNS:www.example.com,DNS:example.com" \
-out example.csr
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

### SNMPv3
Create SNMPv3 User
```bash
net-snmp-create-v3-user -ro \
-A AuthPass -a SHA-256 \
-X EncryptPass -x AES256 snmpuser
```

### SCREEN Tricks

| Description | Command |
|-------------|---------|
|Create new screen session |```screen -S {screen name}```|
|Join screen session |```screen -x {screen name}```|
|Detach from screen  |```screen -d```|
|Re-attach to screen |```screen -r {screen name}```|

Keybord Shortcuts

| Description | Shortcut |
|-------------|----------|
|Detach from screen|```Ctrl + a + Ctrl + d```|   
|Split vertically  |``` Ctrl + a + \|``` |
|Split horizontally|```Ctrl + a + S```|
|Change window|```Ctrl + a + Tab```|
|Start new screen session in window|```Ctrl + a + Ctrl + c```|
|Exit all screen windows|```Ctrl + a + \```|

### Android Debug Bridge (ADB)

| Description | Command |
|-------------|---------|
|Search for devices|```adb devices```|
|List all packages on the phone|```adb shell pm list packages```|
|Remove Android package from phone|```adb shell pm uninstall --user 0 {package}```|
|Take phone screenshot|```adb exec-out screencap -p > ./picture.png```|

### YT-DLP

Download song from youtube to mp3 format
```bash
yt-dlp -x --audio-format 'mp3' {url}
```
