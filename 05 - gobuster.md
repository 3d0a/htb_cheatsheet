## dir enumeration
```bash
 gobuster dir -u http://10.10.11.101 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 150
```

## domain name enumeration
```bash
gobuster vhost -u http://horizontall.htb -w /opt/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -t 150 
```