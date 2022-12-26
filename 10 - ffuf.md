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
```